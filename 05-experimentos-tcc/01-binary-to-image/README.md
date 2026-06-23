# 01-binary-to-image

Conversão de binários executáveis em representações visuais para classificação com CNN.

## Objetivo

Implementar e validar pipeline de conversão de arquivos binários (PE/ELF) em imagens para alimentar a CNN.

## Motivação

CNNs foram projetadas para processar imagens. Binários podem ser visualizados como imagens de bytes, preservando estrutura e padrões locais.

## Abordagens

### 1. Visualização Direta de Bytes
Converter cada byte do binário em pixel grayscale (0-255).

**Processo**:
1. Ler binário como array de bytes
2. Redimensionar para imagem NxN (ex: 128x128, 256x256)
3. Salvar como PNG grayscale

**Pros**: Simples, preserva todos os bytes  
**Contras**: Perde estrutura de seções

### 2. Visualização de Seções
Mapear diferentes seções (.text, .data, .rdata) em canais de cor diferentes.

**Processo**:
1. Parsear PE/ELF
2. Extrair seções importantes
3. Mapear em RGB (R=.text, G=.data, B=.rdata)

**Pros**: Preserva estrutura semântica  
**Contras**: Mais complexo, requer parsing

### 3. Entropy Visualization
Visualizar entropy local em blocos do binário.

**Processo**:
1. Dividir binário em blocos (ex: 256 bytes)
2. Calcular entropy de cada bloco
3. Mapear entropy para intensidade de pixel

**Pros**: Destaca seções comprimidas/encriptadas  
**Contras**: Perde informação de bytes exatos

## Experimentos

### Exp 1.1: Tamanhos de Imagem
Testar diferentes resoluções:
- [ ] 32x32 (rápido, baixa resolução)
- [ ] 64x64 (moderado)
- [ ] 128x128 (bom compromisso)
- [ ] 256x256 (alta resolução, mais lento)

**Métrica**: Accuracy da CNN vs tempo de treino

### Exp 1.2: Grayscale vs RGB
- [ ] Grayscale (1 canal)
- [ ] RGB com seções (3 canais)
- [ ] RGB com entropy + bytes (3 canais)

**Métrica**: Accuracy da CNN, interpretabilidade

### Exp 1.3: Normalização
- [ ] Sem normalização (0-255)
- [ ] Normalização min-max (0-1)
- [ ] Normalização z-score

**Métrica**: Estabilidade do treino, accuracy

## Implementação

### Script Principal
```python
# src/malware_tcc/preprocessing/image_converter.py

class BinaryToImageConverter:
    def __init__(self, img_size=(128, 128), mode='grayscale'):
        self.img_size = img_size
        self.mode = mode
    
    def convert(self, binary_path: str) -> np.ndarray:
        """Converte binário em imagem."""
        pass
    
    def save_image(self, image: np.ndarray, output_path: str):
        """Salva imagem no disco."""
        pass
```

### Pipeline Completo
```bash
# Converter dataset inteiro
python scripts/convert_dataset.py \
    --input data/binaries/ \
    --output data/images/ \
    --size 128 \
    --mode grayscale
```

## Estrutura

```
01-binary-to-image/
├── README.md
├── binary2image.py          # Implementação principal
├── config.yaml              # Configurações
├── convert_dataset.py       # Script para dataset completo
├── visualize_samples.ipynb  # Visualização de amostras
├── results/
│   ├── samples/             # Exemplos de conversões
│   ├── size_comparison.png  # Comparação de tamanhos
│   └── mode_comparison.png  # Comparação de modos
└── docs/
    └── conversion-analysis.md  # Análise detalhada
```

## Visualizações

### Comparação de Tamanhos
Grid mostrando mesmo binário em diferentes resoluções.

### Comparação de Modos
Grid mostrando mesmo binário em grayscale vs RGB vs entropy.

### Exemplos por Família
Mostrar amostras de diferentes famílias de malware.

## Validação

1. **Visual**: Amostras da mesma família devem ter aparência similar
2. **Reversibilidade**: Informação suficiente para classificação?
3. **Performance**: Tempo de conversão aceitável?
4. **Tamanho**: Imagens cabem em memória/disco?

## Entregáveis

- [ ] Script de conversão funcional
- [ ] Notebook com visualizações
- [ ] Análise de diferentes configurações
- [ ] Recomendação de configuração ótima
- [ ] Dataset de imagens completo

## Papers de Referência

- **"Malware Images: Visualization and Automatic Classification"** (Nataraj et al., 2011) - Fundador da área
- **"Deep Learning for Malware Detection based on Image Visualization"** - Variações modernas

## Próximo Experimento

➡️ [02-baseline-ml-classico](../02-baseline-ml-classico/) - Estabelecer baseline com ML clássico
