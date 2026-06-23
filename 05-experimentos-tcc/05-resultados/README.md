# 05-resultados

Consolidação de todos os resultados dos experimentos do TCC.

## Objetivo

Reunir, organizar e apresentar todos os resultados finais dos experimentos de forma clara para inclusão no TCC.

## Estrutura

```
05-resultados/
├── README.md
├── summary.md                    # Resumo executivo de resultados
├── tables/
│   ├── baseline-comparison.csv   # Comparação de baselines
│   ├── cnn-architectures.csv     # Comparação de arquiteturas CNN
│   ├── final-metrics.csv         # Métricas finais consolidadas
│   └── confusion-matrices.csv    # Matrizes de confusão
├── plots/
│   ├── baseline-vs-cnn.png       # Comparação geral
│   ├── training-curves.png       # Curvas de treino
│   ├── confusion-matrix-final.png
│   ├── per-family-performance.png
│   ├── roc-curves.png
│   └── gradcam-examples-grid.png
├── analysis/
│   ├── error-analysis.md         # Análise detalhada de erros
│   ├── statistical-tests.md      # Testes estatísticos (t-test, etc.)
│   └── limitations.md            # Limitações do trabalho
└── notebooks/
    ├── final-results-summary.ipynb    # Notebook consolidado
    └── statistical-analysis.ipynb     # Análises estatísticas
```

## Métricas Consolidadas

### Comparação Final: Baseline vs CNN

| Modelo | Accuracy | Precision | Recall | F1-Score | AUC-ROC | Tempo Treino |
|--------|----------|-----------|--------|----------|---------|--------------|
| Random Forest | ?% | ?% | ?% | ?% | ? | ? |
| SVM (RBF) | ?% | ?% | ?% | ?% | ? | ? |
| XGBoost | ?% | ?% | ?% | ?% | ? | ? |
| **SimpleCNN** | ?% | ?% | ?% | ?% | ? | ? |
| **ResNet-18** | ?% | ?% | ?% | ?% | ? | ? |
| CNN Custom | ?% | ?% | ?% | ?% | ? | ? |

**Melhor Modelo**: [Nome do modelo]  
**Ganho sobre Baseline**: [X]%

### Performance por Família de Malware

| Família | Accuracy | Precision | Recall | F1-Score | Suporte |
|---------|----------|-----------|--------|----------|---------|
| Trojan.Generic | ?% | ?% | ?% | ?% | ? |
| Ransomware | ?% | ?% | ?% | ?% | ? |
| Backdoor | ?% | ?% | ?% | ?% | ? |
| Worm | ?% | ?% | ?% | ?% | ? |
| Adware | ?% | ?% | ?% | ?% | ? |
| ... | ... | ... | ... | ... | ... |

**Melhor Detectada**: [Família com maior F1]  
**Mais Difícil**: [Família com menor F1]

## Análise de Resultados

### 1. Superioridade da CNN

**Hipótese**: CNN supera ML clássico em pelo menos 5% de accuracy  
**Resultado**: [Confirmada ✓ / Refutada ✗]  
**Evidência**: CNN alcançou X% vs baseline Y%

**Discussão**:
- CNN aprende features automaticamente vs features manuais
- Hierarquia espacial captura padrões locais e globais
- Robustez a variações (data augmentation)

### 2. Visualização com Grad-CAM

**Achados**:
- CNN foca principalmente em: [regiões identificadas]
- Padrões comuns por família: [descrição]
- Validação de features relevantes: [discussão]

**Exemplos**:
- Família X: CNN destaca [região Y] → [interpretação de segurança]
- Família Z: Atenção em [região W] → [validação com conhecimento de malware]

### 3. Análise de Erros

**Confusões Mais Comuns**:
1. [Família A] ↔ [Família B]: X casos
   - **Causa provável**: [hipótese baseada em análise]
   - **Similaridade visual**: [evidência de Grad-CAM]
   
2. [Família C] ↔ [Família D]: Y casos
   - **Causa provável**: [hipótese]
   - **Sugestão de melhoria**: [proposta]

**Amostras Difíceis**:
- Samples com [característica X] tendem a ser mal classificados
- Possível solução: [sugestão de trabalho futuro]

### 4. Testes Estatísticos

**t-test (Baseline vs CNN)**:
- Hipótese nula: μ_CNN = μ_baseline
- Resultado: p-value = [valor]
- Conclusão: Diferença [é / não é] estatisticamente significativa (α=0.05)

**McNemar's Test** (predições pareadas):
- Resultado: p-value = [valor]
- Conclusão: [interpretação]

## Visualizações Finais

### 1. Comparação Geral
Gráfico de barras comparando todas as métricas de todos os modelos.

### 2. Curvas de Treino
Loss e accuracy ao longo das epochs para melhor modelo CNN.

### 3. Matriz de Confusão
Matriz de confusão normalizada do melhor modelo no test set.

### 4. Performance por Família
Heatmap ou gráfico de barras mostrando F1-score por família.

### 5. Curvas ROC
Curvas ROC multi-class (one-vs-rest) com AUC.

### 6. Grid Grad-CAM
Grid com exemplos de Grad-CAM de diferentes famílias.

## Limitações do Trabalho

### 1. Dataset
- **Limitação**: Dataset [tamanho, desbalanceamento, antiguidade]
- **Impacto**: [como afeta resultados]
- **Mitigação**: [o que foi feito]

### 2. Generalização
- **Limitação**: Testado apenas em dataset X
- **Impacto**: Desconhecido como performa em malware real/novo
- **Trabalho futuro**: Testar em outros datasets

### 3. Recursos Computacionais
- **Limitação**: Treinamento limitado a [GPU/tempo disponível]
- **Impacto**: Não testou arquiteturas maiores ou mais epochs
- **Mitigação**: Focou em arquiteturas comprovadas

### 4. Adversarial Robustness
- **Limitação**: Não testou contra ataques adversariais
- **Impacto**: CNN pode ser vulnerável a modificações mínimas
- **Trabalho futuro**: Avaliar robustez adversarial

## Contribuições do Trabalho

1. **Validação empírica**: CNN supera ML clássico em [X]% para malware classification
2. **Interpretabilidade**: Grad-CAM revela que CNN foca em [regiões relevantes]
3. **Pipeline reproduzível**: Código e experimentos documentados para replicação
4. **Análise comparativa**: Comparação sistemática de múltiplas abordagens
5. **Insights de segurança**: [Descobertas sobre padrões de malware]

## Trabalhos Futuros

### Curto Prazo
- [ ] Testar em outros datasets (SOREL-20M, BODMAS)
- [ ] Arquiteturas mais avançadas (EfficientNet, Vision Transformers)
- [ ] Ensemble de CNN + ML clássico

### Médio Prazo
- [ ] Adversarial training e robustez
- [ ] Multi-modal learning (imagem + features estáticas)
- [ ] Zero-shot learning para famílias desconhecidas

### Longo Prazo
- [ ] Deploy em produção (API, monitoramento)
- [ ] Interpretabilidade avançada (concept activation vectors)
- [ ] Few-shot learning para novas ameaças

## Checklist para TCC

- [ ] Todas as tabelas de métricas preenchidas
- [ ] Todas as figuras geradas em alta resolução
- [ ] Análise de erros documentada
- [ ] Testes estatísticos calculados
- [ ] Limitações claramente expostas
- [ ] Trabalhos futuros listados
- [ ] Código comentado e organizado
- [ ] Resultados reproduzíveis (seeds fixadas)
- [ ] Documentação completa (READMEs, comments)

## Como Usar Este Diretório

Este diretório é a **fonte de verdade** para todos os números, gráficos e tabelas do TCC.

**Fluxo**:
1. Experimentos geram resultados brutos
2. Notebooks consolidam e processam
3. Figuras e tabelas finais vão para `plots/` e `tables/`
4. Análises vão para `analysis/`
5. **TCC cita diretamente daqui**

**Exemplo de Citação no TCC**:
> "Conforme apresentado na Tabela X, a CNN ResNet-18 alcançou accuracy de [X]%, superando o melhor baseline (Random Forest com [Y]%) em [Z] pontos percentuais."

---

**Status**: 🔴 Aguardando experimentos  
**Última Atualização**: [Data]  
**Responsável**: [Seu Nome]
