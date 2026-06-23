# Experimento: [Nome do Experimento]

**Data Início**: YYYY-MM-DD  
**Última Atualização**: YYYY-MM-DD  
**Status**: [ ] Planejado [ ] Em Progresso [ ] Concluído [ ] Bloqueado

## Objetivo

Descrição clara do que este experimento pretende validar ou descobrir.

## Hipótese

- **H0 (Hipótese Nula)**: [O que esperamos que NÃO aconteça]
- **H1 (Hipótese Alternativa)**: [O que esperamos que aconteça]

## Motivação

Por que este experimento é importante para o TCC? Qual lacuna ele preenche?

## Configuração do Experimento

### Dataset
- **Nome**: 
- **Tamanho**: 
- **Classes**: 
- **Split**: train (X%), val (Y%), test (Z%)
- **Pré-processamento**: 

### Modelo/Abordagem
- **Tipo**: 
- **Arquitetura**: 
- **Hiperparâmetros**:
  - Learning rate: 
  - Batch size: 
  - Epochs: 
  - Optimizer: 
  - Loss function: 

### Ambiente
- **Hardware**: 
- **Software**: Python X.X, PyTorch X.X
- **Tempo estimado**: 

## Baseline

Qual é a performance mínima esperada (baseline) para comparação?
- Baseline 1: [método simples] - X% accuracy
- Baseline 2: [método existente] - Y% accuracy

## Implementação

### Etapas
1. [ ] Preparar dataset
2. [ ] Implementar modelo
3. [ ] Configurar treino
4. [ ] Executar experimento
5. [ ] Coletar métricas
6. [ ] Analisar resultados
7. [ ] Visualizar findings

### Código
Localização dos scripts e notebooks:
- Script principal: `src/experimentos/[nome]/train.py`
- Notebook exploratório: `notebooks/exploratorios/[nome].ipynb`
- Configuração: `configs/[nome].yaml`

## Resultados

### Métricas Quantitativas

| Métrica | Baseline | Proposto | Melhoria |
|---------|----------|----------|----------|
| Accuracy | X% | Y% | +Z% |
| Precision | X% | Y% | +Z% |
| Recall | X% | Y% | +Z% |
| F1-Score | X% | Y% | +Z% |

### Confusion Matrix

```
[Inserir imagem ou representação da matriz de confusão]
```

### Visualizações

- [ ] Curvas de loss
- [ ] Curvas de accuracy
- [ ] Exemplos de predições corretas
- [ ] Exemplos de predições incorretas
- [ ] Grad-CAM ou visualizações XAI

## Análise

### O que funcionou?
- Observação 1
- Observação 2

### O que não funcionou?
- Problema 1
- Problema 2

### Insights
- Insight 1: [descoberta importante]
- Insight 2: [padrão observado]

## Conclusões

Resumo dos achados e se a hipótese foi validada ou refutada.

## Próximos Passos

- [ ] Testar variação X
- [ ] Otimizar hiperparâmetro Y
- [ ] Comparar com abordagem Z
- [ ] Documentar para o TCC

## Problemas e Bloqueios

- [ ] Problema 1: [descrição] - Status: [resolvido/pendente]
- [ ] Problema 2: [descrição] - Status: [resolvido/pendente]

## Referências

Papers, tutoriais ou código que inspiraram este experimento:
- Referência 1
- Referência 2

---

**Tags**: #experimento #cnn #baseline #pytorch  
**Arquivos Relacionados**: 
- Dataset: `05-experimentos-tcc/00-dataset/`
- Código: `src/malware_tcc/`
- Resultados: `05-experimentos-tcc/05-resultados/[nome]/`
