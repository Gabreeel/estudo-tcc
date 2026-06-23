# 05-experimentos-tcc

Experimentos estruturados do TCC. Cada experimento segue o [template-experimento.md](../templates/template-experimento.md) e é reproduzível.

## Pipeline do TCC

```
00-dataset → 01-binary-to-image → 02-baseline → 03-cnn → 04-xai → 05-resultados
```

## Estrutura dos Experimentos

### 00-dataset
**Objetivo**: Preparar dataset para experimentos

- [ ] Definir dataset público (EMBER, MalImg, etc.)
- [ ] Documentar processo de coleta
- [ ] Criar splits train/val/test
- [ ] Análise exploratória
- [ ] Estatísticas descritivas

**Entregáveis**:
- `dataset-info.md`: Documentação completa
- `eda.ipynb`: Análise exploratória
- `splits/`: Arquivos com splits

### 01-binary-to-image
**Objetivo**: Converter binários em representações visuais

- [ ] Implementar conversão binário → imagem
- [ ] Testar diferentes tamanhos (32x32, 64x64, 128x128)
- [ ] Testar diferentes formatos (grayscale, RGB)
- [ ] Validar qualidade visual
- [ ] Criar visualizações

**Entregáveis**:
- `binary2image.py`: Script de conversão
- `visualizations.ipynb`: Notebook com exemplos
- `samples/`: Imagens de exemplo

### 02-baseline-ml-classico
**Objetivo**: Estabelecer baseline com ML clássico

- [ ] Extrair features clássicas (n-grams, imports, entropy)
- [ ] Treinar Random Forest
- [ ] Treinar SVM
- [ ] Avaliar métricas
- [ ] Comparar abordagens

**Entregáveis**:
- `extract_features.py`: Extração de features
- `train_baseline.py`: Treino dos modelos
- `results/`: Métricas e visualizações
- `baseline-report.md`: Relatório de resultados

### 03-cnn-pytorch
**Objetivo**: Treinar CNN para classificação de imagens de binários

- [ ] Implementar arquitetura CNN
- [ ] Configurar pipeline de treino
- [ ] Treinar modelo
- [ ] Validar e testar
- [ ] Comparar com baseline

**Entregáveis**:
- `model.py`: Arquitetura da CNN
- `train.py`: Script de treino
- `config.yaml`: Configuração de hiperparâmetros
- `checkpoints/`: Modelos salvos
- `cnn-report.md`: Relatório de resultados

### 04-gradcam-xai
**Objetivo**: Interpretar decisões da CNN com Grad-CAM

- [ ] Implementar Grad-CAM
- [ ] Gerar visualizações
- [ ] Analisar regiões importantes
- [ ] Validar interpretabilidade
- [ ] Documentar insights

**Entregáveis**:
- `gradcam.py`: Implementação Grad-CAM
- `visualize_xai.ipynb`: Notebook com análises
- `heatmaps/`: Visualizações geradas
- `xai-analysis.md`: Análise dos resultados

### 05-resultados
**Objetivo**: Consolidar e apresentar todos os resultados

- [ ] Métricas finais de todos os experimentos
- [ ] Comparação baseline vs CNN
- [ ] Análise de erros
- [ ] Visualizações para TCC
- [ ] Discussão e conclusões

**Entregáveis**:
- `final-results.md`: Consolidação de resultados
- `plots/`: Gráficos para TCC
- `tables/`: Tabelas de métricas
- `discussion.md`: Discussão dos achados

## Reprodutibilidade

Cada experimento deve ser **100% reproduzível**:
1. Documentar ambiente (Python version, bibliotecas)
2. Fixar seeds aleatórias
3. Versionar datasets (hashes)
4. Configurar via arquivos YAML/JSON
5. Logar métricas (Weights & Biases, TensorBoard)

## Como Executar

```bash
# Preparar ambiente
cd 05-experimentos-tcc/
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
pip install -r requirements.txt

# Executar pipeline completo
bash run_pipeline.sh

# Ou experimentos individuais
cd 01-binary-to-image/
python binary2image.py --config config.yaml
```

## Importante

- **NÃO** commitar datasets grandes (usar .gitignore)
- **NÃO** commitar modelos treinados (usar .gitignore)
- **NÃO** commitar amostras reais de malware
- **SIM** commitar código, configs, notebooks vazios
- **SIM** documentar tudo no formato do template
