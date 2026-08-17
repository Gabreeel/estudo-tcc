# TCC: Classificação de Famílias de Malware usando Deep Learning e Representação Visual de Binários

[![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.0+-red.svg)](https://pytorch.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Em%20Desenvolvimento-yellow.svg)]()

**Autor**: Gabriel  
**Instituição**: Universidade de Brasília (UnB) 
**Orientador**: -  
**Previsão de Defesa**: Novembro 2027

---

##  Resumo do Projeto

Este repositório contém todos os estudos, experimentos e desenvolvimento do meu Trabalho de Conclusão de Curso (TCC) sobre **classificação automática de famílias de malware** usando **Deep Learning** e **representação visual de binários**.

### Problema
A identificação manual de variantes e famílias de malware é trabalhosa, demorada e requer expertise especializado. Com o crescimento exponencial de ameaças, sistemas automáticos são essenciais.

### Solução Proposta
Conversão de arquivos binários (PE/ELF) em **imagens** e uso de **CNNs (Convolutional Neural Networks)** para classificação automática, eliminando necessidade de feature engineering manual.

### Diferencial
- **End-to-end learning**: CNN aprende features automaticamente
- **Explainability**: Uso de Grad-CAM para interpretar decisões
- **Comparação rigorosa**: Baseline com ML clássico vs Deep Learning
- **Pipeline reproduzível**: Código, datasets, e experimentos documentados

---

##  Objetivos

### Geral
Desenvolver e avaliar um sistema de classificação automática de famílias de malware baseado em CNNs e representação visual de binários.

### Específicos
1. Implementar pipeline de conversão binário → imagem
2. Estabelecer baseline com ML clássico (Random Forest, SVM)
3. Treinar e otimizar CNN para classificação multi-classe
4. Aplicar técnicas de XAI (Grad-CAM) para interpretabilidade
5. Comparar performance CNN vs baseline
6. Analisar robustez e limitações da abordagem

---

##  Estrutura do Repositório

```
estudo-tcc/
├── 00-planejamento/           # Planejamento e gestão do projeto
├── 01-cursos/                 # Material de estudos organizados
│   ├── baixo-nivel/           # Assembly, x86/x64, arquitetura
│   └── ia-e-dados/            # ML, DL, PyTorch, CNNs
├── 02-fundamentos/            # Conhecimento consolidado
│   ├── baixo-nivel/           # Registradores, PE/ELF, Assembly
│   ├── malware-analysis/      # Técnicas de análise
│   └── ia-e-dados/            # CNNs, métricas, PyTorch
├── 03-papers/                 # Revisão bibliográfica
│   └── fichamentos/           # Fichamentos de papers
├── 04-laboratorios/           # Prática hands-on
│   ├── crackmes/              # Desafios de reversing
│   ├── ghidra-scripts/        # Automação de análise
│   └── feature-extraction/    # Extração de features
├── 05-experimentos-tcc/       # Experimentos do TCC
│   ├── 00-dataset/            # Preparação do dataset
│   ├── 01-binary-to-image/    # Conversão binário → imagem
│   ├── 02-baseline-ml-classico/ # Baseline (RF, SVM)
│   ├── 03-cnn-pytorch/        # CNN principal
│   ├── 04-gradcam-xai/        # Interpretabilidade
│   └── 05-resultados/         # Consolidação de resultados
├── src/                       # Código reutilizável (pacote Python)
│   └── malware_tcc/           # Módulos do projeto
│       ├── preprocessing/     # Pré-processamento
│       ├── features/          # Extração de features
│       ├── models/            # Definições de modelos
│       ├── evaluation/        # Métricas e XAI
│       └── utils/             # Utilitários
├── notebooks/                 # Jupyter notebooks
│   ├── exploratorios/         # Exploração inicial
│   ├── prototipos/            # Protótipos de modelos
│   └── finais/                # Notebooks polidos
├── reports/                   # Documentos formais
│   ├── proposta-tcc/          # Proposta inicial
│   ├── apresentacoes/         # Slides de apresentações
│   └── relatorio-final/       # TCC completo (LaTeX)
├── assets/                    # Recursos visuais
│   ├── images/                # Diagramas, screenshots
│   └── plots/                 # Gráficos e visualizações
├── templates/                 # Templates de documentação
├── .gitignore                 # Exclusões do Git
├── ROADMAP.md                 # Timeline do projeto
├── GLOSSARIO.md               # Glossário de termos
├── REFERENCIAS.md             # Referências bibliográficas
└── README.md                  # Este arquivo
```

**Ver**: [ROADMAP.md](ROADMAP.md) para timeline detalhada e [00-planejamento/](00-planejamento/) para gestão do projeto.

---

##  Pipeline do TCC

```
┌──────────────┐
│   Binários   │
│  (PE/ELF)    │
└──────┬───────┘
       │
       ├─────────────────────────┐
       ↓                         ↓
┌──────────────┐        ┌──────────────────┐
│  Conversão   │        │    Extração      │
│ Binário→IMG  │        │   de Features    │
└──────┬───────┘        └────────┬─────────┘
       │                         │
       ↓                         ↓
┌──────────────┐        ┌──────────────────┐
│     CNN      │        │  ML Clássico     │
│  (PyTorch)   │        │  (Baseline)      │
└──────┬───────┘        └────────┬─────────┘
       │                         │
       ├─────────────────────────┘
       ↓
┌──────────────┐
│ Classificação│
│  de Família  │
└──────┬───────┘
       │
       ↓
┌──────────────┐
│   Grad-CAM   │
│     (XAI)    │
└──────────────┘
```

---

##  Papers Principais

### Visual Classification
1. **Malware Images: Visualization and Automatic Classification** (Nataraj et al., 2011) ⭐⭐⭐⭐⭐
2. **Deep Learning for Classification of Malware System Call Sequences** (Kolosnjaji et al., 2016)
3. **Visualizing Malware Features using Deep Learning** (Gibert et al., 2019)

### End-to-End Learning
4. **MalConv: Malware Detection by Executing a Neural Network on Raw Bytes** (Raff et al., 2018)
5. **EMBER: An Open Dataset for Training Static PE Malware Machine Learning Models** (Anderson & Roth, 2018) ⭐⭐⭐⭐⭐
6. **Deep Convolutional Malware Classifiers Can Learn from Raw Executables** (Krčál et al., 2018)

### Adversarial ML e Robustez
7. **Exploring Adversarial Examples in Malware Detection** (Suciu et al., 2019)
8. **Adversarial Examples on Discrete Sequences for Beating Malware Detection** (Kreuk et al., 2018)
9. **Intriguing Properties of Adversarial ML Attacks in the Problem Space** (Pierazzi et al., 2020)

### Explainability (XAI)
10. **Grad-CAM: Visual Explanations from Deep Networks** (Selvaraju et al., 2017) ⭐⭐⭐⭐⭐
11. **A Unified Approach to Interpreting Model Predictions (SHAP)** (Lundberg & Lee, 2017)
12. **Explaining Deep Learning Models with Constrained Adversarial Examples** (Melis et al., 2018)

### Multi-modal e Graph-based
13. **Mass Classification of Malware Based on Semantic Information Fusion** (Peng et al., 2019)
14. **Deep4MalDroid: Android Malware Detection Based on System Call Graphs** (Hou et al., 2017)
15. **HinDroid: Android Malware Detection Based on Heterogeneous Information Network** (Yan et al., 2020)

### Surveys e State-of-the-Art
16. **A Survey on Malware Detection Using Data Mining Techniques** (Ye et al., 2017)
17. **Survey of Machine Learning Techniques for Malware Analysis** (Ucci et al., 2019)
18. **Deep Learning Approach for Intelligent Intrusion Detection System** (Vinayakumar et al., 2019)

**Ver**: [REFERENCIAS.md](REFERENCIAS.md) e [03-papers/](03-papers/) para detalhes e fichamentos.

---

##  Stack Tecnológico

### Análise de Malware
- **Ghidra**: Reverse engineering e análise estática
- **IDA Pro**: Disassembly profissional (licença educacional)
- **pefile / pyelftools**: Parsing de executáveis
- **YARA**: Detecção baseada em regras

### Machine Learning e Deep Learning
- **PyTorch**: Framework principal de DL
- **scikit-learn**: ML clássico (baseline)
- **NumPy / Pandas**: Manipulação de dados
- **Matplotlib / Seaborn**: Visualização

### Explainability e Avaliação
- **pytorch-grad-cam**: Implementação Grad-CAM
- **captum**: Framework de interpretabilidade (Facebook Research)
- **Weights & Biases**: Tracking de experimentos (opcional)
- **TensorBoard**: Visualização de treino

### Ambiente de Desenvolvimento
- **Python 3.10+**: Linguagem principal
- **Jupyter Notebooks**: Exploração interativa
- **VS Code**: IDE principal
- **Git / GitHub**: Controle de versão

---

##  Status do Projeto

### Fase 1: Fundamentos (Jul 2026 - Out 2026) 🟢 **EM PROGRESSO**
- [x] Estruturar repositório profissionalmente
- [x] Criar templates de documentação
- [ ] Completar curso OST2 Architecture (50% concluído)
- [ ] Completar curso Udemy ML (40% concluído)
- [ ] Fichar 10 papers principais
- [ ] Consolidar fundamentos em `02-fundamentos/`

### Fase 2: Revisão Bibliográfica (Nov 2026 - Dez 2026) ⚪ **PLANEJADO**
- [ ] Fichar 18 papers principais
- [ ] Criar matriz de comparação
- [ ] Identificar gaps de pesquisa
- [ ] Definir contribuição do TCC
- [ ] Escrever capítulo de trabalhos relacionados

### Fase 3: Laboratórios Práticos (Jan 2027 - Fev 2027) ⚪ **PLANEJADO**
- [ ] Resolver 10+ crackmes
- [ ] Desenvolver scripts Ghidra
- [ ] Implementar extração de features
- [ ] Praticar debugging e análise

### Fase 4: Experimentos (Mar 2027 - Jun 2027) ⚪ **PLANEJADO**
- [ ] Preparar dataset (EMBER ou MalImg)
- [ ] Implementar conversão binário → imagem
- [ ] Treinar baseline (RF, SVM)
- [ ] Treinar CNN (SimpleCNN, ResNet)
- [ ] Aplicar Grad-CAM
- [ ] Consolidar resultados

### Fase 5: Escrita e Defesa (Jul 2027 - Mar 2027) ⚪ **PLANEJADO**
- [ ] Escrever TCC completo
- [ ] Preparar apresentação
- [ ] Revisar e ajustar
- [ ] **Defesa: Março 2027**

**Ver**: [ROADMAP.md](ROADMAP.md) para detalhes de cada fase.

---

## 📖 Como Usar Este Repositório

### Para Estudar
1. Navegue por [01-cursos/](01-cursos/) para material de estudos
2. Consulte [02-fundamentos/](02-fundamentos/) para referência rápida
3. Use [templates/](templates/) para padronizar anotações

### Para Revisar Literatura
1. Veja lista de papers na seção acima
2. Leia fichamentos em [03-papers/fichamentos/](03-papers/fichamentos/)
3. Consulte [REFERENCIAS.md](REFERENCIAS.md) para bibliografia completa

### Para Reproduzir Experimentos
1. Siga instruções em [05-experimentos-tcc/](05-experimentos-tcc/)
2. Cada experimento tem README próprio com setup
3. Código reutilizável está em [src/malware_tcc/](src/malware_tcc/)

### Para Entender Decisões
1. Leia [00-planejamento/](00-planejamento/) para contexto do projeto
2. Consulte [GLOSSARIO.md](GLOSSARIO.md) para terminologia
3. Veja [notebooks/](notebooks/) para análises interativas

---

##  Contribuição e Colaboração

Este é um projeto acadêmico individual, mas **feedback é bem-vindo**!

- **Issues**: Reporte bugs ou sugira melhorias
- **Discussões**: Use GitHub Discussions para trocar ideias
- **Citação**: Se usar código ou ideias, por favor cite este repositório

---

##  Licença

Este projeto está licenciado sob a **MIT License** - veja [LICENSE](LICENSE) para detalhes.

**Nota**: Datasets de malware podem ter restrições de uso. Sempre respeite termos de serviço e legislação local.

---

##  Contato

**Gabriel**  
📧 Email: [seu-email@dominio.com]  
🐙 GitHub: [@Gabreeel](https://github.com/Gabreeel)  
🔗 LinkedIn: [seu-linkedin]

**Orientador**: - 
📧 Email: -

---

##  Agradecimentos

- **OpenSecurityTraining2**: Curso gratuito de arquitetura de alta qualidade
- **Udemy**: Cursos de ML e Deep Learning
- **Comunidade de Segurança**: Datasets públicos e ferramentas open-source
- **PyTorch Community**: Framework excelente e documentação

---

##  Recursos Adicionais

### Livros
- *Practical Malware Analysis* (Sikorski & Honig, 2012)
- *The Art of Memory Forensics* (Ligh et al., 2014)
- *Deep Learning* (Goodfellow, Bengio, Courville, 2016)
- *Hands-On Machine Learning with Scikit-Learn, Keras & TensorFlow* (Géron, 2019)

### Datasets Públicos
- **EMBER**: 1.1M samples com features pré-extraídas
- **MalImg**: 9,339 malware images (25 famílias)
- **SOREL-20M**: 20M samples (mais recente)
- **VirusShare / Malware Bazaar**: Coleta de amostras

### Ferramentas
- **Ghidra**: https://ghidra-sre.org/
- **IDA Free**: https://hex-rays.com/ida-free/
- **pefile**: https://github.com/erocarrera/pefile
- **YARA**: https://virustotal.github.io/yara/

---

**Última atualização**: Junho 2026  
**Versão do repositório**: 2.0 (Reorganização Profissional)

---

⭐ **Se este repositório foi útil, considere dar uma estrela!**
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
