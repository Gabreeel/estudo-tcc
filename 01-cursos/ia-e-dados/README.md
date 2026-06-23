# ia-e-dados

Cursos de Machine Learning, Deep Learning e análise de dados.

## Cursos

### udemy-python-data-science-ml
**Status**: 🟢 Em Progresso  
**Fonte**: Udemy - Python for Data Science and Machine Learning Bootcamp  
**Descrição**: Python, NumPy, Pandas, Matplotlib, Scikit-Learn, ML clássico

**Progresso**: 25/165 aulas  
**Aplicação no TCC**: Baseline com ML clássico (Random Forest, SVM), análise exploratória

📁 [Ver pasta](./udemy-python-data-science-ml/)

### udemy-pytorch-deep-learning-cv
**Status**: ⚪ Planejado  
**Fonte**: Udemy - PyTorch for Deep Learning and Computer Vision  
**Descrição**: PyTorch, CNNs, Transfer Learning, Computer Vision

**Progresso**: 0/120 aulas  
**Aplicação no TCC**: Implementação da CNN, arquitetura do modelo principal

📁 [Ver pasta](./udemy-pytorch-deep-learning-cv/)

## Próximos Cursos

- **Explainable AI (XAI)**: Interpretabilidade de modelos
- **Advanced Deep Learning Architectures**: ResNet, EfficientNet, ViT
- **MLOps**: Deploy e monitoramento de modelos

## Conexão com TCC

Conhecimento de IA e dados é o core do projeto:
1. **Baseline com ML clássico**: Random Forest, SVM com features engineered
2. **CNN para classificação**: Modelo principal do TCC
3. **Análise exploratória**: Entender dataset, distribuição de classes
4. **Avaliação**: Métricas (accuracy, precision, recall, F1, ROC-AUC)
5. **XAI**: Grad-CAM para interpretar decisões da CNN

## Pipeline do TCC

```
Binários → Features Estáticas → ML Clássico (Baseline)
                              ↓
Binários → Imagens → CNN → Classificação
                        ↓
                   Grad-CAM → Interpretação
```

## Recursos

### Livros
- *Hands-On Machine Learning with Scikit-Learn, Keras & TensorFlow* (Aurélien Géron)
- *Deep Learning* (Goodfellow, Bengio, Courville)
- *Deep Learning with PyTorch* (Eli Stevens)

### Papers Fundamentais
- AlexNet (2012) - CNNs para ImageNet
- ResNet (2015) - Redes residuais profundas
- Grad-CAM (2017) - Visualização de atenção em CNNs

### Datasets
- **ImageNet**: Classificação de imagens natural (baseline)
- **EMBER**: Malware features dataset
- **MalImg**: Malware images dataset
- **SOREL-20M**: Large-scale malware dataset
