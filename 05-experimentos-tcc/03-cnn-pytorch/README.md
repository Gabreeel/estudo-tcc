# 03-cnn-pytorch

Implementar e treinar CNN com PyTorch para classificação de imagens de malware.

## Objetivo

Superar o baseline de ML clássico usando CNN que aprende features automaticamente das imagens de binários.

## Motivação

CNNs eliminam necessidade de feature engineering manual:
- **Automatic feature learning**: Aprende padrões relevantes dos dados
- **Spatial hierarchy**: Captura estrutura local e global
- **Transfer learning**: Pode usar pesos pré-treinados

## Arquiteturas a Testar

### 1. CNN Simples Baseline
```python
class SimpleCNN(nn.Module):
    def __init__(self, num_classes):
        super().__init__()
        self.features = nn.Sequential(
            nn.Conv2d(1, 32, kernel_size=3, padding=1),
            nn.ReLU(),
            nn.MaxPool2d(2),
            nn.Conv2d(32, 64, kernel_size=3, padding=1),
            nn.ReLU(),
            nn.MaxPool2d(2),
            nn.Conv2d(64, 128, kernel_size=3, padding=1),
            nn.ReLU(),
            nn.MaxPool2d(2),
        )
        self.classifier = nn.Sequential(
            nn.Flatten(),
            nn.Linear(128 * 16 * 16, 512),
            nn.ReLU(),
            nn.Dropout(0.5),
            nn.Linear(512, num_classes)
        )
    
    def forward(self, x):
        x = self.features(x)
        x = self.classifier(x)
        return x
```

### 2. ResNet-18 Adaptado
- Usar arquitetura ResNet-18 pré-treinada no ImageNet
- Fine-tuning para malware classification
- Modificar primeiro layer para grayscale (1 canal)

### 3. CNN Customizada
- Inspirada em papers de malware visualization
- Arquitetura otimizada para padrões de binários
- Múltiplas scales de receptive fields

## Pipeline de Treino

```
Imagens → DataLoader → CNN → Loss → Optimizer → Backprop
           ↓
    Data Augmentation
```

### Data Loading
```python
# src/malware_tcc/data/dataloader.py

from torch.utils.data import Dataset, DataLoader
from torchvision import transforms

class MalwareImageDataset(Dataset):
    def __init__(self, image_dir, transform=None):
        self.image_paths = glob(f'{image_dir}/**/*.png')
        self.transform = transform
    
    def __getitem__(self, idx):
        img = Image.open(self.image_paths[idx])
        label = self.get_label(self.image_paths[idx])
        if self.transform:
            img = self.transform(img)
        return img, label

# Transforms
transform = transforms.Compose([
    transforms.Resize((128, 128)),
    transforms.ToTensor(),
    transforms.Normalize(mean=[0.5], std=[0.5])
])

train_loader = DataLoader(
    MalwareImageDataset('data/train', transform),
    batch_size=32,
    shuffle=True
)
```

### Training Loop
```python
# scripts/train_cnn.py

def train_epoch(model, loader, criterion, optimizer):
    model.train()
    total_loss = 0
    for images, labels in loader:
        images, labels = images.to(device), labels.to(device)
        
        optimizer.zero_grad()
        outputs = model(images)
        loss = criterion(outputs, labels)
        loss.backward()
        optimizer.step()
        
        total_loss += loss.item()
    return total_loss / len(loader)

# Treinamento completo
for epoch in range(num_epochs):
    train_loss = train_epoch(model, train_loader, criterion, optimizer)
    val_loss = evaluate(model, val_loader, criterion)
    
    print(f'Epoch {epoch}: Train Loss={train_loss:.4f}, Val Loss={val_loss:.4f}')
    
    # Save checkpoint
    if val_loss < best_val_loss:
        save_checkpoint(model, f'checkpoints/best_model.pth')
```

## Experimentos

### Exp 3.1: Arquiteturas
- [ ] CNN Simples (3 conv layers)
- [ ] CNN Média (5 conv layers)
- [ ] ResNet-18 (transfer learning)
- [ ] ResNet-18 (from scratch)

**Métrica**: Accuracy, tempo de treino

### Exp 3.2: Hiperparâmetros
- [ ] Learning rate: [1e-4, 1e-3, 1e-2]
- [ ] Batch size: [16, 32, 64]
- [ ] Optimizer: [Adam, SGD, AdamW]
- [ ] Epochs: [50, 100, 200]

**Métrica**: Validation accuracy

### Exp 3.3: Regularização
- [ ] Dropout: [0.3, 0.5, 0.7]
- [ ] Weight decay: [1e-4, 1e-5]
- [ ] Data augmentation: [sim, não]
- [ ] Batch normalization: [sim, não]

**Métrica**: Overfitting gap (train - val accuracy)

### Exp 3.4: Data Augmentation
- [ ] Rotação: ±15°
- [ ] Flip horizontal
- [ ] Random crop
- [ ] Brightness adjustment

**Métrica**: Validation accuracy, robustez

## Configuração

```yaml
# config.yaml

model:
  architecture: 'SimpleCNN'
  num_classes: 25
  input_size: [128, 128]
  
training:
  batch_size: 32
  epochs: 100
  learning_rate: 0.001
  optimizer: 'Adam'
  weight_decay: 1e-4
  
data:
  train_dir: 'data/images/train'
  val_dir: 'data/images/val'
  test_dir: 'data/images/test'
  augmentation: true
  
logging:
  tensorboard: true
  save_freq: 10
  checkpoint_dir: 'checkpoints/'
```

## Estrutura

```
03-cnn-pytorch/
├── README.md
├── model.py                 # Definições de arquiteturas
├── train.py                 # Script de treino
├── evaluate.py              # Avaliação no test set
├── config.yaml              # Configuração
├── requirements.txt         # Dependências PyTorch
├── notebooks/
│   ├── model-visualization.ipynb     # Visualizar arquitetura
│   └── training-analysis.ipynb       # Análise de treino
├── checkpoints/
│   ├── best_model.pth
│   ├── epoch_50.pth
│   └── final_model.pth
├── logs/
│   └── tensorboard/         # Logs TensorBoard
└── results/
    ├── training-curves.png
    ├── confusion-matrix.png
    ├── per-class-accuracy.png
    └── metrics.csv
```

## Métricas Esperadas

### Comparação Baseline vs CNN

| Modelo | Accuracy | Precision | Recall | F1-Score | Tempo Treino |
|--------|----------|-----------|--------|----------|--------------|
| RF (Baseline) | 85% | 83% | 82% | 82% | 5 min |
| SimpleCNN | 90% | 89% | 88% | 88% | 2h |
| ResNet-18 | 93% | 92% | 91% | 91% | 4h |

**Meta**: Superar baseline em pelo menos 5% de accuracy

## Monitoring

### TensorBoard
```bash
tensorboard --logdir logs/tensorboard/
```

Visualizar:
- Training/Validation loss
- Training/Validation accuracy
- Learning rate schedule
- Grad norms (detectar vanishing/exploding gradients)

### Weights & Biases (Opcional)
- Melhor tracking e comparação de experimentos
- Hyperparameter sweep automático
- Model versioning

## Entregáveis

- [ ] Modelos CNN treinados e salvos
- [ ] Curvas de treino (loss e accuracy)
- [ ] Matriz de confusão no test set
- [ ] Comparação com baseline
- [ ] Análise de erros (quais classes são confundidas)
- [ ] Relatório de hiperparâmetros ótimos

## Papers de Referência

- **"Deep Learning for Malware Detection based on Image Visualization"** (diversas variações)
- **"Deep Convolutional Neural Networks for Image Classification: A Comprehensive Review"** (arquiteturas)
- **"Visualizing and Understanding Convolutional Networks"** (Zeiler & Fergus, 2014)

## Próximo Experimento

➡️ [04-gradcam-xai](../04-gradcam-xai/) - Interpretar decisões da CNN com Grad-CAM
