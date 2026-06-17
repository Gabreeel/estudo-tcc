# IA e Dados: Machine Learning e Deep Learning

## Visão Geral

Estudos de Inteligência Artificial, Machine Learning e Ciência de Dados aplicados ao projeto de classificação de malware. Objetivos:

1. **Baseline Clássico:** Treinar modelos tradicionais (Random Forest, SVM) em features estáticas como comparação
2. **Deep Learning:** Implementar CNNs para classificação visual de binários
3. **Avaliação Rigorosa:** Evitar armadilhas comuns (overfitting, data leakage, métricas enganosas)
4. **Pesquisa:** Preparar para contribuições acadêmicas em ML aplicado a segurança

---

## Conteúdo

### [Udemy-Machine-Learning/](Udemy-Machine-Learning/)
Fundamentos de ML clássico
- Algoritmos supervisionados (KNN, SVM, Decision Trees, Random Forest)
- Unsupervised learning (K-Means, PCA)
- Avaliação de modelos (confusion matrix, cross-validation)
- Feature engineering e pré-processamento

### [A Adicionar]
- **Deep-Learning-CNNs/**: CNNs para visão computacional (PyTorch/TensorFlow)
- **NLP-for-Malware/**: Representação de strings/API calls como texto (opcional)
- **GNNs/**: Graph Neural Networks para CFGs (avançado)

---

## Objetivos de Aprendizado

### Fundamentos de Machine Learning
- [x] Diferença entre aprendizado supervisionado vs não-supervisionado
- [x] Train/validation/test split (jamais testar em dados vistos!)
- [ ] Métricas de avaliação: accuracy, precision, recall, F1-score, AUC-ROC
- [ ] Cross-validation (K-Fold) para datasets pequenos
- [ ] Hyperparameter tuning (Grid Search, Random Search)

### Deep Learning para Imagens
- [ ] **Arquitetura de CNNs:** Convolutional layers, pooling, fully connected
- [ ] **Transfer Learning:** Usar modelos pré-treinados (ResNet, VGG) e fine-tuning
- [ ] **Data Augmentation:** Rotação, flip, zoom (menos relevante para binários, mas importante conhecer)
- [ ] **Frameworks:** PyTorch (preferido) ou TensorFlow/Keras

### Tópicos Avançados
- [ ] **Explainability (XAI):** Grad-CAM, SHAP, LIME para entender decisões do modelo
- [ ] **Adversarial Examples:** Como atacar/defender modelos de malware
- [ ] **Multi-modal Learning:** Combinar imagens + grafos + features estáticas
- [ ] **Few-Shot Learning:** Classificar com poucos exemplos (relevante para malware raro)

---

## Ferramentas e Bibliotecas

### Ambiente de Desenvolvimento
```bash
# Python 3.10+ recomendado
python -m venv venv-malware
source venv-malware/bin/activate  # Linux/macOS
# venv-malware\Scripts\activate   # Windows

# Dependências essenciais
pip install numpy pandas matplotlib seaborn jupyter
pip install scikit-learn
pip install torch torchvision  # PyTorch (ou tensorflow)
pip install pillow  # Manipulação de imagens
```

### Bibliotecas-Chave

**Machine Learning Clássico:**
- `scikit-learn` - Todos os algoritmos tradicionais
- `pandas` - Manipulação de dados tabulares
- `numpy` - Operações matriciais
- `matplotlib`, `seaborn` - Visualização

**Deep Learning:**
- `PyTorch` - Framework modular e intuitivo [preferido]
- `TensorFlow/Keras` - Alternativa (mais abstrato)
- `torchvision` - Modelos pré-treinados e datasets
- `tensorboard` - Visualização de treinamento

**Malware Específico:**
- `pefile` - Parser de arquivos PE (Windows)
- `lief` - Parser de PE/ELF/Mach-O
- `capstone` - Disassembler em Python (features avançadas)

**Explainability:**
- `captum` - Grad-CAM e attribution methods (PyTorch)
- `shap` - Valores Shapley para ML
- `lime` - Local Interpretable Model-agnostic Explanations

---

## Pipeline do Projeto

### Fase 1: Baseline Clássico (ML Tradicional)

```python
# 1. Extrair features estáticas de executáveis
import pefile

def extract_features(pe_path):
    pe = pefile.PE(pe_path)
    return {
        'entropy': pe.sections[0].get_entropy(),
        'num_sections': len(pe.sections),
        'num_imports': len(pe.DIRECTORY_ENTRY_IMPORT),
        'size': os.path.getsize(pe_path),
        'has_debug': pe.DIRECTORY_ENTRY_DEBUG is not None
    }

# 2. Treinar Random Forest
from sklearn.ensemble import RandomForestClassifier
clf = RandomForestClassifier(n_estimators=100, max_depth=10)
clf.fit(X_train, y_train)

# 3. Avaliar
from sklearn.metrics import classification_report
print(classification_report(y_test, clf.predict(X_test)))
```

**Objetivo:** Estabelecer baseline (~80-85% accuracy no Malware Kaggle Dataset)

---

### Fase 2: CNNs em Imagens Binárias

```python
# 1. Converter binário para imagem
def binary_to_image(bin_path, width=256):
    with open(bin_path, 'rb') as f:
        data = f.read()
    arr = np.frombuffer(data, dtype=np.uint8)
    size = int(len(arr) ** 0.5) + 1
    arr = np.pad(arr, (0, size**2 - len(arr)))
    img = arr.reshape(size, size)
    return Image.fromarray(img)

# 2. Criar dataset PyTorch
class MalwareImageDataset(Dataset):
    def __init__(self, image_dir, labels):
        self.images = [os.path.join(image_dir, f) for f in os.listdir(image_dir)]
        self.labels = labels
        self.transform = transforms.Compose([
            transforms.Resize((224, 224)),
            transforms.ToTensor()
        ])
    
    def __getitem__(self, idx):
        img = Image.open(self.images[idx]).convert('L')  # Grayscale
        return self.transform(img), self.labels[idx]

# 3. Treinar CNN simples
model = models.resnet18(pretrained=True)
model.fc = nn.Linear(512, num_classes)  # Ajustar para num de famílias

criterion = nn.CrossEntropyLoss()
optimizer = optim.Adam(model.parameters(), lr=0.001)

for epoch in range(20):
    for images, labels in train_loader:
        outputs = model(images)
        loss = criterion(outputs, labels)
        loss.backward()
        optimizer.step()
```

**Objetivo:** Superar baseline (90-95% accuracy esperado)

---

### Fase 3: Explainability (Diferencial Competitivo!)

```python
# Grad-CAM para visualizar onde a CNN está "olhando"
from captum.attr import LayerGradCam

model.eval()
grad_cam = LayerGradCam(model, model.layer4)

attribution = grad_cam.attribute(input_img, target=family_class)
# Plotar heatmap sobreposto à imagem original

# Resultado: CNN foca na seção .text? No header? Em regiões de payload?
```

**Objetivo:** Publicar insights sobre *o que CNNs aprendem* de malware (paper material!)

---

## Recursos de Aprendizado

### Cursos Online

**Machine Learning:**
- **Andrew Ng - Machine Learning (Coursera)** - Fundamentos matemáticos rigorosos
- **Fast.ai - Practical Deep Learning** - Top-down approach (código primeiro)
- **Udemy - Machine Learning A-Z** (já em progresso)

**Deep Learning:**
- **Stanford CS231n** - CNNs for Visual Recognition (lectures no YouTube)
- **PyTorch Tutorials** - Documentação oficial (excelente!)
- **Deep Learning Specialization (Coursera)** - Andrew Ng

### Livros Essenciais

1. **"Hands-On Machine Learning" - Aurélien Géron** ⭐ (scikit-learn + TensorFlow)
2. **"Deep Learning" - Goodfellow, Bengio, Courville** (A Bíblia, mas denso)
3. **"Introduction to Machine Learning with Python" - Müller & Guido**
4. **"Dive into Deep Learning" - Aston Zhang et al.** (gratuito online!)

### Papers Fundamentais

**Malware + ML:**
1. **Nataraj et al. (2011)** - "Malware Images: Visualization and Automatic Classification" [PIONEIRO]
2. **Raff et al. (2018)** - "MalConv: Malware Detection by Executing a Neural Network on Raw Bytes"
3. **Anderson & Roth (2018)** - "Ember: An Open Dataset for Training Static PE Malware ML Models"
4. **Gibert et al. (2020)** - "Adversarial Examples in Malware Detection"

**Explainability (para seu diferencial!):**
5. **Selvaraju et al. (2017)** - "Grad-CAM: Visual Explanations from Deep Networks"
6. **Lundberg & Lee (2017)** - "A Unified Approach to Interpreting Model Predictions" (SHAP)

---

## Exercícios Progressivos

### Checkpoint 1: Fundamentos ML (Semana 1-2)
- [ ] Completar módulos do Udemy-Machine-Learning
- [ ] Treinar Random Forest no Iris dataset
- [ ] Implementar K-Fold cross-validation manual
- [ ] Plotar confusion matrix e ROC curve

### Checkpoint 2: Baseline de Malware (Semana 3-4)
- [ ] Implementar extrator de features PE com `pefile`
- [ ] Baixar Malware Kaggle Dataset ou Ember
- [ ] Treinar Random Forest/XGBoost em features estáticas
- [ ] Meta: >80% accuracy como baseline

### Checkpoint 3: CNNs em Imagens (Semana 5-7)
- [ ] Converter 1000 samples em imagens PNG
- [ ] Implementar dataset PyTorch customizado
- [ ] Treinar CNN do zero (arquitetura simples: 3 conv layers)
- [ ] Treinar ResNet18 com transfer learning
- [ ] Meta: >90% accuracy

### Checkpoint 4: Explainability (Semana 8)
- [ ] Aplicar Grad-CAM em 50 amostras corretamente classificadas
- [ ] Identificar padrões: CNN foca em headers? Payload? Padding?
- [ ] Escrever seção de análise qualitativa no TCC

---

## Conexão com Mestrado

### Por que Tsukuba Valoriza Este Perfil?

**Research Groups Relevantes:**
- **Prof. Koshiba (Cryptography & Security):** Publicações em adversarial ML, segurança teórica
- **Prof. Miyamoto (Software Security):** Análise de malware, program analysis
- **Prof. Sakurai (Computer Science):** ML applications, data science

**Requisitos esperados:**
1. Rigor científico: Não apenas "funcionou", mas por que funcionou
2. Comparação com estado da arte: Seu modelo vs MalConv, Ember, trabalhos recentes
3. Contribuição nova: Explainability, adversarial robustness, multi-modal fusion
4. Comunicação: Papers em inglês (IEEE, ACM), apresentações em conferências

**Estratégia:**
- Publicar em workshop (AISec, RAID Poster Session) **ANTES** de aplicar
- Escrever research proposal detalhado (3-5 páginas) alinhado com papers do professor
- Demonstrar proficiência em inglês (TOEFL/IELTS) + japonês básico (opcional mas ajuda)

---

## Critérios de Proficiência

Você estará pronto para o TCC quando:

1. Explicar diferença entre overfitting e underfitting e demonstrar com exemplos
2. Implementar pipeline completo de ML do zero
3. Treinar CNN em novo dataset com >85% accuracy em 1 dia
4. Interpretar Grad-CAM e explicar o que o modelo aprendeu
5. Comparar seu trabalho com 3+ papers recentes criticamente

---

## Progresso

**Status Atual:** 🟡 Em andamento (Udemy-Machine-Learning)  
**Próximos Passos:**
1. Completar fundamentos de ML (scikit-learn)
2. Implementar baseline de features estáticas PE
3. Começar tutorial PyTorch oficial
4. Converter 1000 malware samples em imagens
5. Treinar primeira CNN (ResNet18 com transfer learning)
