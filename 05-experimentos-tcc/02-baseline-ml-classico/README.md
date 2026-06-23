# 02-baseline-ml-classico

Estabelecer baseline de performance com Machine Learning clássico usando features engineered.

## Objetivo

Criar baseline de comparação para a abordagem CNN. ML clássico com features crafted manualmente serve como ponto de referência.

## Motivação

Antes de deep learning, classificação de malware era feita com:
1. Extração manual de features relevantes
2. Modelos clássicos (Random Forest, SVM, etc.)

Este baseline responde: **"A CNN aprende algo além do que features clássicas capturam?"**

## Features a Extrair

### 1. Features Estáticas Básicas
- **Tamanho do arquivo** (bytes)
- **Entropy** (global e por seção)
- **Número de seções**
- **Tamanho de seções** (.text, .data, .rdata, etc.)

### 2. Imports e Exports
- **APIs importadas** (CreateProcess, WriteFile, RegSetValue, etc.)
- **DLLs carregadas** (kernel32.dll, ntdll.dll, ws2_32.dll)
- **Frequência de imports suspeitos**

### 3. Strings e Caracteres
- **Número de strings** (printable)
- **URLs e IPs** (regex matching)
- **Registry keys** mencionadas
- **Strings suspeitas** (password, admin, decrypt, etc.)

### 4. Header Information (PE)
- **Timestamp** de compilação
- **Subsystem** (GUI, Console, Native)
- **Architecture** (x86, x64, ARM)
- **Linker version**

### 5. Byte-level Features
- **N-grams de bytes** (unigram, bigram, trigram)
- **Histogram de bytes** (frequência 0-255)
- **Entropy local** (por blocos)

## Modelos a Testar

### 1. Random Forest
- **Pros**: Robusto, não requer normalização, feature importance
- **Contras**: Pode overfittar com muitas features
- **Hiperparâmetros**: n_estimators, max_depth, min_samples_split

### 2. Support Vector Machine (SVM)
- **Pros**: Bom para espaços de alta dimensão
- **Contras**: Sensível a escala, lento com muitos dados
- **Hiperparâmetros**: kernel (linear, RBF), C, gamma

### 3. Gradient Boosting (XGBoost/LightGBM)
- **Pros**: Alta performance, regularização built-in
- **Contras**: Mais lento que RF
- **Hiperparâmetros**: learning_rate, n_estimators, max_depth

### 4. Logistic Regression
- **Pros**: Simples, interpretável, rápido
- **Contras**: Assume linearidade
- **Hiperparâmetros**: C, penalty

## Pipeline

```
Binário → Feature Extraction → Normalização → Modelo → Predição
```

### Feature Extraction
```python
# src/malware_tcc/features/static_features.py

def extract_features(binary_path: str) -> np.ndarray:
    features = {}
    
    # 1. Tamanho e entropy
    features['file_size'] = get_file_size(binary_path)
    features['entropy'] = calculate_entropy(binary_path)
    
    # 2. PE parsing
    pe = pefile.PE(binary_path)
    features['num_sections'] = len(pe.sections)
    features['num_imports'] = count_imports(pe)
    
    # 3. Strings
    strings = extract_strings(binary_path)
    features['num_strings'] = len(strings)
    features['has_url'] = any(re.match(URL_REGEX, s) for s in strings)
    
    # 4. N-grams
    ngrams = extract_ngrams(binary_path, n=2)
    features.update(ngrams)
    
    return np.array(list(features.values()))
```

### Training
```python
# scripts/train_baseline.py

from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import train_test_split
from sklearn.metrics import classification_report

# Carregar features
X, y = load_features('data/features.csv')
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

# Treinar
clf = RandomForestClassifier(n_estimators=100, max_depth=20)
clf.fit(X_train, y_train)

# Avaliar
y_pred = clf.predict(X_test)
print(classification_report(y_test, y_pred))
```

## Experimentos

### Exp 2.1: Feature Selection
- [ ] Todas as features (~2000)
- [ ] Top 100 features (feature importance)
- [ ] Top 50 features
- [ ] Features manuais apenas (~20)

**Métrica**: Accuracy vs número de features

### Exp 2.2: Comparação de Modelos
- [ ] Random Forest
- [ ] SVM
- [ ] XGBoost
- [ ] Logistic Regression

**Métrica**: Accuracy, Precision, Recall, F1, tempo de treino

### Exp 2.3: Hiperparâmetros
- [ ] Grid Search para RF
- [ ] Grid Search para SVM
- [ ] Comparar com defaults

**Métrica**: Accuracy no validation set

## Estrutura

```
02-baseline-ml-classico/
├── README.md
├── extract_features.py       # Extração de features
├── train_baseline.py         # Treino dos modelos
├── evaluate_baseline.py      # Avaliação
├── config.yaml               # Configurações
├── notebooks/
│   ├── feature-analysis.ipynb      # Análise de features
│   └── model-comparison.ipynb      # Comparação de modelos
├── results/
│   ├── confusion-matrix-rf.png
│   ├── confusion-matrix-svm.png
│   ├── feature-importance.png
│   └── metrics.csv
└── docs/
    └── baseline-report.md     # Relatório completo
```

## Métricas de Avaliação

| Modelo | Accuracy | Precision | Recall | F1-Score | Tempo Treino |
|--------|----------|-----------|--------|----------|--------------|
| RF     | ?        | ?         | ?      | ?        | ?            |
| SVM    | ?        | ?         | ?      | ?        | ?            |
| XGBoost| ?        | ?         | ?      | ?        | ?            |
| LogReg | ?        | ?         | ?      | ?        | ?            |

## Feature Importance

Top 10 features mais importantes (Random Forest):

1. ?
2. ?
3. ...

## Entregáveis

- [ ] Script de extração de features
- [ ] Modelos treinados e salvos
- [ ] Matriz de confusão para cada modelo
- [ ] Feature importance analysis
- [ ] Relatório comparativo
- [ ] Recomendação de melhor modelo baseline

## Papers de Referência

- **EMBER**: Elastic Malware Benchmark (Anderson & Roth, 2018)
- **"Intelligent Malware Detection Using Obfuscation Invariant Feature Learning"** (Islam et al., 2016)

## Próximo Experimento

➡️ [03-cnn-pytorch](../03-cnn-pytorch/) - CNN para superar baseline
