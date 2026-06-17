# Udemy Machine Learning - Fundamentos

## Sobre o Curso

Curso de fundamentos de Machine Learning cobrindo algoritmos supervisionados, não-supervisionados e técnicas de pré-processamento para o projeto de classificação de malware.

---

## Objetivos de Aprendizado

### Conhecimentos-Chave
- **Pré-processamento:** Normalização, encoding, tratamento de missing values
- **Modelos Supervisionados:** Regressão, Classificação (KNN, SVM, Decision Trees, Random Forest)
- **Modelos Não-Supervisionados:** Clustering (K-Means, DBSCAN), PCA
- **Avaliação:** Confusion matrix, precision, recall, F1-score, ROC-AUC
- **Engenharia de Features:** Seleção e extração de características relevantes

### Relevância para Análise de Malware
- **Feature Engineering:** Extrair características de binários (entropy, strings, imports)
- **Baseline Clássico:** Comparar CNNs com Random Forest/SVM em features estáticas
- **Clustering:** Descobrir novas famílias de malware não-rotuladas
- **Avaliação Rigorosa:** Evitar overfitting em datasets desbalanceados

---

## Estrutura do Material

```
Udemy-Machine-Learning/
├── notebooks/         # Jupyter notebooks de exercícios (a criar)
├── datasets/          # Datasets de prática (Iris, Titanic, etc.)
├── modelos/           # Modelos treinados salvos (pickle/joblib)
├── notas/             # Anotações de conceitos-chave (a criar)
└── README.md          # Este arquivo
```

---

## Conteúdo Programático

### Módulo 1: Fundamentos
- [ ] Diferença entre ML supervisionado vs não-supervisionado
- [ ] Train/test split e validação cruzada
- [ ] Overfitting vs underfitting
- [ ] Bias-variance tradeoff

### Módulo 2: Pré-processamento
- [ ] StandardScaler vs MinMaxScaler
- [ ] Encoding categórico (One-Hot, Label Encoding)
- [ ] Tratamento de outliers
- [ ] Feature scaling (essencial para CNNs!)

### Módulo 3: Algoritmos de Classificação
- [ ] K-Nearest Neighbors (KNN)
- [ ] Support Vector Machines (SVM)
- [ ] Decision Trees e Random Forest
- [ ] Naive Bayes
- [ ] Logistic Regression

### Módulo 4: Avaliação de Modelos
- [ ] Confusion Matrix (TP, FP, TN, FN)
- [ ] Precision, Recall, F1-Score
- [ ] ROC Curve e AUC
- [ ] Cross-validation (K-Fold)
- [ ] Grid Search e Hyperparameter Tuning

### Módulo 5: Unsupervised Learning
- [ ] K-Means Clustering
- [ ] DBSCAN
- [ ] PCA (Principal Component Analysis)
- [ ] t-SNE para visualização

### Módulo 6: Ensemble Methods
- [ ] Bagging vs Boosting
- [ ] Random Forest
- [ ] AdaBoost, Gradient Boosting
- [ ] XGBoost (opcional)

---

## Aplicação para o TCC

### Como Integrar no Projeto de Malware

**1. Baseline Clássico (antes de CNNs):**
```python
# Extrair features estáticas de executáveis
features = [
    'entropy',
    'tamanho_arquivo',
    'num_sections',
    'num_imports',
    'tem_upx',
    'ratio_bytes_null'
]

# Treinar Random Forest
from sklearn.ensemble import RandomForestClassifier
clf = RandomForestClassifier(n_estimators=100)
clf.fit(X_train, y_train)
```

**2. Comparação com Deep Learning:**
- Usar Random Forest como baseline (accuracy ~85%)
- Comparar com CNN em imagens (accuracy esperado ~90-95%)
- Paper relevante: Raff et al. (2018) comparou MalConv (DL) vs Ember (Gradient Boosting)

**3. Clustering de Malware Desconhecido:**
```python
# Descobrir famílias em samples não-rotulados
from sklearn.cluster import KMeans
kmeans = KMeans(n_clusters=10)
clusters = kmeans.fit_predict(X_unknown)
```

---

## Ferramentas e Bibliotecas

### Python Essenciais
```bash
pip install scikit-learn pandas numpy matplotlib seaborn jupyter
```

### Bibliotecas Principais
- **scikit-learn:** Todos os algoritmos clássicos de ML
- **pandas:** Manipulação de dados tabulares
- **numpy:** Operações matriciais
- **matplotlib/seaborn:** Visualização de dados
- **joblib:** Salvar/carregar modelos treinados

---

## Datasets de Prática

### Para Aprendizado
1. Iris Dataset (classificação multi-classe) - Incluído no scikit-learn
2. **Titanic** (classificação binária com features categóricas)
3. **MNIST** (imagens, preparação para CNNs)

### Para Malware (futuramente)
1. **PE Feature Dataset** - Features extraídas de executáveis
2. **Ember Dataset** - 1M+ samples com features estáticas
3. **Android Malware Dataset** (alternativa ao Windows)

---

## Exercícios-Chave

### Checkpoint 1: Classificação Básica
- [ ] Treinar KNN no Iris dataset
- [ ] Aplicar StandardScaler e comparar resultados
- [ ] Gerar confusion matrix e calcular F1-score

### Checkpoint 2: Árvores de Decisão
- [ ] Treinar Decision Tree no Titanic
- [ ] Visualizar a árvore gerada
- [ ] Comparar com Random Forest (ensemble)

### Checkpoint 3: Avaliação Rigorosa
- [ ] Implementar 5-fold cross-validation
- [ ] Aplicar Grid Search para tuning de hiperparâmetros
- [ ] Plotar ROC curve com AUC

### Checkpoint 4: Clustering
- [ ] Aplicar K-Means em dataset não-rotulado
- [ ] Determinar K ótimo com Elbow Method
- [ ] Visualizar clusters com PCA

---

## Recursos Adicionais

### Cursos Complementares
- **Andrew Ng - Machine Learning (Coursera)** - Mais matemático
- **Fast.ai - Practical Deep Learning** - Transição para DL

### Livros
- **"Introduction to Machine Learning with Python" - Müller & Guido**
- **"Hands-On Machine Learning" - Aurélien Géron** (essencial!)
- **"Pattern Recognition and Machine Learning" - Bishop** (avançado)

### Papers Relevantes para Malware
- **Schultz et al. (2001)** - "Data Mining Methods for Detection of New Malicious Executables" (primeiro uso de ML em malware)
- **Ember (2018)** - "Gradient Boosting com Features PE"
- **Raff et al. (2018)** - "MalConv: Learning Directly from Bytes"

---

## Objetivos de Conclusão

Ao completar este módulo:
- Implementar pipelines completos de ML (pré-processamento → treino → avaliação)
- Escolher o algoritmo apropriado para diferentes problemas
- Interpretar métricas de avaliação (não apenas accuracy)
- Evitar erros comuns (data leakage, overfitting em test set)
- Aplicar ML clássico como baseline para o TCC

---

## ✅ Progresso Atual

**Status:** 🟢 Iniciado  
**Módulo Atual:** [Indicar módulo]  
**Próximo:** Aplicar conceitos em dataset de malware (Ember ou próprio)
