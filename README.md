# Estudos para TCC: Classificação Multi-modal de Malware

## Tema do TCC

**Classificação Avançada de Famílias de Malware Usando Deep Learning e Representação Visual de Binários**

### Objetivo
Desenvolver um sistema de classificação automática de famílias de malware combinando:
- Representação visual de binários como imagens
- CNNs para identificação de padrões
- Análise estática sem execução do malware

### Motivação
A identificação manual de variantes de malware é trabalhosa e demorada. Este projeto automatiza a classificação através de visão computacional aplicada a executáveis.

### Pipeline Técnico
1. **Coleta:** Dataset público (Malware Bazaar, Kaggle Malware Dataset)
2. **Pré-processamento:** Conversão de executáveis (.exe, ELF) em imagens PNG (8-bit grayscale)
3. **Treinamento:** CNN para classificação de famílias
4. **Avaliação:** Métricas de accuracy, precision, recall e F1-score
5. **Validação:** Análise manual de amostras com Ghidra/IDA

### Possíveis Extensões
- [ ] Multi-modal fusion (imagens + CFG graphs)
- [ ] Explainability via Grad-CAM/SHAP
- [ ] Robustez contra adversarial examples
- [ ] Comparação com MalConv, Ember (SOTA)

---

## Estrutura de Estudos

### [Baixo-Nivel/](Baixo-Nivel/)
Fundamentos de arquitetura de computadores, Assembly e engenharia reversa
- OST2-Architecture-1001: Curso de arquitetura x86/x64 e Assembly
- Crackmes: Exercícios práticos de reversing

### [IA-e-Dados/](IA-e-Dados/)
Machine Learning, Deep Learning e análise de dados
- Udemy-Machine-Learning: Fundamentos de ML supervisionado/não-supervisionado
- CNNs: Redes convolucionais para visão computacional (a adicionar)
- PyTorch/TensorFlow: Frameworks de deep learning (a adicionar)

---

## Metas de Aprendizado

### Conhecimentos Técnicos Necessários
- [x] Assembly x86/x64 (leitura de disassembly)
- [ ] Estrutura PE (Windows) e ELF (Linux)
- [ ] Ferramentas: Ghidra, IDA Pro, radare2
- [x] Python (scikit-learn, pandas, numpy)
- [ ] Deep Learning: CNNs, Transfer Learning
- [ ] PyTorch ou TensorFlow/Keras
- [ ] Datasets: Manipulação de malware com segurança

### Bibliografia Essencial

**Fundamentos de Classificação Visual:**
1. Nataraj et al. (2011) - "Malware Images: Visualization and Automatic Classification"
2. Saxe & Berlin (2015) - "Deep Neural Network Based Malware Detection Using Two Dimensional Binary Program Features"
3. Gibert et al. (2018) - "Deep Learning for Malware Detection: A Survey"

**Abordagens End-to-End:**
4. Raff et al. (2018) - "MalConv: Malware Detection by Executing a Neural Network on Raw Bytes"
5. Anderson & Roth (2018) - "EMBER: An Open Dataset for Training Static PE Malware Machine Learning Models"
6. Krčál et al. (2018) - "Deep Convolutional Malware Classifiers Can Learn from Raw Executables and Labels Only"

**Adversarial ML e Robustez:**
7. Gibert et al. (2020) - "Adversarial Examples in Deep Learning for Multivariate Time Series Regression"
8. Suciu et al. (2019) - "Exploring Adversarial Examples in Malware Detection"
9. Kreuk et al. (2018) - "Adversarial Examples on Discrete Sequences for Beating Whole-Binary Malware Detection"

**Explainability (XAI):**
10. Selvaraju et al. (2017) - "Grad-CAM: Visual Explanations from Deep Networks via Gradient-based Localization"
11. Lundberg & Lee (2017) - "A Unified Approach to Interpreting Model Predictions" (SHAP)
12. Melis et al. (2018) - "Explaining Deep Learning Models with Constrained Adversarial Examples"

**Multi-modal e Graph-based:**
13. Peng et al. (2019) - "MCSMGS: Mass Classification of Malware Based on Semantic Information Fusion and Deep Graph Networks"
14. Hou et al. (2017) - "Deep4MalDroid: A Deep Learning Framework for Android Malware Detection Based on Linux Kernel System Call Graphs"
15. Yan et al. (2020) - "HinDroid: An Intelligent Android Malware Detection System Based on Structured Heterogeneous Information Network"

**Surveys e State-of-the-Art:**
16. Ye et al. (2017) - "A Survey on Malware Detection Using Data Mining Techniques"
17. Ucci et al. (2019) - "Survey of Machine Learning Techniques for Malware Analysis"
18. Vinayakumar et al. (2019) - "Deep Learning Approach for Intelligent Intrusion Detection System"

---

## Objetivo Acadêmico

**Mestrado na Universidade de Tsukuba**
- Research groups: Security & Cryptography, AI Applications
- Professores: Prof. Koshiba (Cryptography), Prof. Miyamoto (Software Security)
- Preparação: Publicação em workshops (IEEE S&P, AISec), perfil em ML + Security

---

## Progresso

**Fase Atual:** Revisão de fundamentos (Assembly + ML)  
**Próximos Passos:**
1. Completar curso OST2-Architecture-1001
2. Implementar script de conversão binário → imagem
3. Explorar datasets disponíveis (Malware Bazaar, Kaggle)
4. Baseline: CNN simples em PyTorch
5. Escrever proposta formal de TCC

---

## Ferramentas e Ambiente

```bash
# Análise Estática
- Ghidra / IDA Pro
- PE-bear, PEiD
- strings, objdump

# Machine Learning
- Python 3.10+
- PyTorch / TensorFlow
- scikit-learn, pandas, matplotlib

# Segurança
- VM isolada (VirtualBox/VMware)
- REMnux (distro para RE)
```

---

## Referências e Recursos

- [Malware Bazaar](https://bazaar.abuse.ch/)
- [Awesome Malware Analysis](https://github.com/rshipp/awesome-malware-analysis)
- [MalConv Paper](https://arxiv.org/abs/1710.09435)
- [PyTorch Documentation](https://pytorch.org/docs/stable/index.html)
