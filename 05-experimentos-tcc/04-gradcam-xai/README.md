# 04-gradcam-xai

Interpretar decisões da CNN usando Grad-CAM (Gradient-weighted Class Activation Mapping) e outras técnicas de Explainable AI.

## Objetivo

Responder a pergunta: **"O que a CNN está olhando quando classifica um malware?"**

CNNs são "caixas-pretas". XAI (Explainable AI) torna decisões interpretáveis.

## Motivação

1. **Validação científica**: Verificar se CNN aprende padrões corretos
2. **Confiança**: Mostrar que decisões são baseadas em features relevantes
3. **Debugging**: Identificar se modelo está "trapaceando" (shortcuts)
4. **Insight**: Descobrir quais partes de binários são discriminativas

## Técnicas de XAI

### 1. Grad-CAM (Principal)
Grad-CAM gera heatmap mostrando regiões importantes para classificação.

**Como funciona**:
1. Forward pass até camada convolucional alvo
2. Backward pass do score da classe predita
3. Calcular gradientes em relação a feature maps
4. Ponderar feature maps pelos gradientes
5. Gerar heatmap e sobrepor em imagem original

```python
# src/malware_tcc/evaluation/xai.py

import torch
import torch.nn.functional as F

class GradCAM:
    def __init__(self, model, target_layer):
        self.model = model
        self.target_layer = target_layer
        self.gradients = None
        self.activations = None
        
        # Register hooks
        target_layer.register_forward_hook(self.save_activation)
        target_layer.register_backward_hook(self.save_gradient)
    
    def save_activation(self, module, input, output):
        self.activations = output.detach()
    
    def save_gradient(self, module, grad_input, grad_output):
        self.gradients = grad_output[0].detach()
    
    def generate_heatmap(self, image, class_idx=None):
        # Forward pass
        output = self.model(image)
        
        if class_idx is None:
            class_idx = output.argmax(dim=1)
        
        # Backward pass
        self.model.zero_grad()
        class_score = output[:, class_idx]
        class_score.backward()
        
        # Calculate weights
        weights = self.gradients.mean(dim=(2, 3), keepdim=True)
        
        # Weighted combination
        cam = (weights * self.activations).sum(dim=1, keepdim=True)
        cam = F.relu(cam)
        cam = F.interpolate(cam, size=image.shape[2:], mode='bilinear')
        cam = cam - cam.min()
        cam = cam / cam.max()
        
        return cam.squeeze().cpu().numpy()
```

### 2. Saliency Maps
Gradient simples da imagem de entrada.

```python
def saliency_map(model, image, target_class):
    image.requires_grad = True
    output = model(image)
    output[0, target_class].backward()
    saliency = image.grad.abs()
    return saliency.squeeze().cpu().numpy()
```

### 3. Guided Backpropagation
Versão modificada do backprop que preserva apenas gradientes positivos.

### 4. Attention Maps (se usar ViT)
Se usar Vision Transformers, visualizar attention weights diretamente.

## Visualizações

### 1. Heatmap Sobreposto
```python
import matplotlib.pyplot as plt
import cv2

def overlay_heatmap(image, heatmap, alpha=0.4):
    # Normalizar imagem original
    img = (image - image.min()) / (image.max() - image.min())
    img = (img * 255).astype(np.uint8)
    
    # Aplicar colormap ao heatmap
    heatmap = (heatmap * 255).astype(np.uint8)
    heatmap_colored = cv2.applyColorMap(heatmap, cv2.COLORMAP_JET)
    
    # Sobrepor
    overlay = cv2.addWeighted(img, 1-alpha, heatmap_colored, alpha, 0)
    return overlay

# Plotar
fig, axes = plt.subplots(1, 3, figsize=(15, 5))
axes[0].imshow(original_image, cmap='gray')
axes[0].set_title('Original')
axes[1].imshow(heatmap, cmap='jet')
axes[1].set_title('Grad-CAM Heatmap')
axes[2].imshow(overlay)
axes[2].set_title('Overlay')
plt.savefig('gradcam_example.png')
```

### 2. Grid de Amostras
Mostrar múltiplas amostras de diferentes classes com heatmaps.

### 3. Comparação Corretas vs Incorretas
Visualizar heatmaps de predições corretas e incorretas para entender erros.

## Experimentos

### Exp 4.1: Validação de Relevância
- [ ] Gerar Grad-CAM para 100 amostras do test set
- [ ] Verificar se regiões ativas fazem sentido
- [ ] Comparar com conhecimento de malware analysis
- [ ] Identificar padrões comuns por família

**Objetivo**: Validar que CNN aprende features corretas

### Exp 4.2: Análise de Erros
- [ ] Visualizar heatmaps de predições incorretas
- [ ] Identificar se CNN está focando em regiões erradas
- [ ] Comparar heatmaps de amostras confundidas

**Objetivo**: Entender por que CNN erra

### Exp 4.3: Comparação de Técnicas
- [ ] Grad-CAM
- [ ] Saliency Maps
- [ ] Guided Backpropagation
- [ ] Grad-CAM++

**Objetivo**: Escolher melhor técnica para visualização

### Exp 4.4: Insights de Segurança
- [ ] Identificar bytecode patterns discriminativos
- [ ] Mapear regiões importantes de volta para seções do binário
- [ ] Documentar features aprendidas automaticamente

**Objetivo**: Descobrir conhecimento novo sobre malware

## Estrutura

```
04-gradcam-xai/
├── README.md
├── gradcam.py               # Implementação Grad-CAM
├── visualize_xai.py         # Script de visualização
├── analyze_errors.py        # Análise de erros
├── config.yaml              # Configuração
├── notebooks/
│   ├── gradcam-exploration.ipynb    # Exploração inicial
│   └── xai-analysis.ipynb           # Análise completa
├── results/
│   ├── heatmaps/
│   │   ├── correct/         # Predições corretas
│   │   └── incorrect/       # Predições incorretas
│   ├── grid_visualizations.png
│   ├── per_family_patterns.png
│   └── error_analysis.png
└── docs/
    └── xai-insights.md      # Documentação de insights
```

## Análise Esperada

### Padrões por Família
Identificar regiões características:
- **Trojan.Generic**: Foco em seção .text (código malicioso)
- **Ransomware**: Atenção em imports de criptografia
- **Backdoor**: Destaque em network calls
- **Worm**: Padrões de propagação

### Validação Científica
- CNN foca em **header PE/ELF**? ❌ (Não deveria)
- CNN foca em **seção .text**? ✅ (Esperado)
- CNN foca em **imports suspeitos**? ✅ (Bom sinal)
- CNN foca em **overlay data**? 🤔 (Interessante, investigar)

## Entregáveis

- [ ] Implementação Grad-CAM funcional
- [ ] Grid de visualizações (≥50 amostras)
- [ ] Análise de padrões por família
- [ ] Análise de erros com heatmaps
- [ ] Documento de insights (xai-insights.md)
- [ ] Visualizações para TCC (figuras de alta qualidade)

## Papers de Referência

- **"Grad-CAM: Visual Explanations from Deep Networks via Gradient-based Localization"** (Selvaraju et al., 2017) - Paper original
- **"Grad-CAM++: Improved Visual Explanations for Deep Convolutional Networks"** (Chattopadhyay et al., 2018)
- **"Visualizing and Understanding Convolutional Networks"** (Zeiler & Fergus, 2014)
- **"Explainable AI for Malware Detection: A Survey"** - Surveys de XAI em segurança

## Ferramentas Úteis

- **pytorch-grad-cam**: Implementação pronta de múltiplas técnicas XAI
- **captum**: Framework de interpretabilidade do PyTorch (Facebook Research)
- **LIME**: Local Interpretable Model-agnostic Explanations

## Próximo Experimento

➡️ [05-resultados](../05-resultados/) - Consolidar todos os resultados e análises finais
