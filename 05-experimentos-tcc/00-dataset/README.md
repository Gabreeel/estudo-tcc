# 00-dataset

Preparação, análise exploratória e documentação do dataset do TCC.

## Objetivo

Obter, preparar e documentar o dataset que será usado em todos os experimentos subsequentes.

## Dataset Escolhido

**Nome**: [A definir - EMBER, MalImg, ou custom]  
**Fonte**: [Link para download]  
**Tamanho**: [X amostras, Y classes]  
**Licença**: [Tipo de licença]

## Estrutura

### raw/
Dados brutos baixados (NÃO commitar ao Git):
- Arquivos originais sem modificação
- Documentação oficial do dataset

### processed/
Dados processados prontos para uso:
- Splits train/val/test
- Metadados organizados
- Índices e labels

### docs/
Documentação do dataset:
- **dataset-info.md**: Descrição completa
- **statistics.md**: Estatísticas descritivas
- **eda.ipynb**: Análise exploratória

## Tarefas

- [ ] Pesquisar datasets disponíveis
- [ ] Escolher dataset adequado ao escopo
- [ ] Baixar e verificar integridade
- [ ] Análise exploratória inicial
- [ ] Criar splits train/val/test (70/15/15 ou 60/20/20)
- [ ] Documentar distribuição de classes
- [ ] Verificar desbalanceamento
- [ ] Calcular estatísticas (média, std, tamanho)
- [ ] Gerar visualizações

## Critérios de Escolha

- **Acessibilidade**: Disponível publicamente ou mediante solicitação
- **Tamanho**: Suficiente para treinar CNN (idealmente > 10k amostras)
- **Balanceamento**: Distribuição de classes razoável
- **Documentação**: Bem documentado e usado em papers
- **Formato**: Binários reais ou features já extraídas?
- **Famílias**: Número de famílias de malware (multi-class)

## Datasets Candidatos

### EMBER (Elastic Malware Benchmark for Empowering Researchers)
- **Tamanho**: 1.1M samples
- **Formato**: Features pré-extraídas (2381 features)
- **Classes**: Binary (malware/benign) + multi-class (famílias)
- **Pros**: Grande, bem documentado, usado em muitos papers
- **Contras**: Features já extraídas (não temos binários)

### MalImg
- **Tamanho**: 9,339 samples
- **Formato**: Imagens de binários (grayscale)
- **Classes**: 25 famílias de malware
- **Pros**: Imagens prontas, perfeito para CNN
- **Contras**: Menor, mais antigo (2011)

### SOREL-20M
- **Tamanho**: 20M samples
- **Formato**: Binários reais + features
- **Classes**: Binary (malware/benign)
- **Pros**: Muito grande, recente, abrangente
- **Contras**: Muito grande para TCC, requer muito armazenamento

### Custom (Coletar próprio)
- **Tamanho**: A definir
- **Formato**: Binários reais
- **Fontes**: VirusTotal, Malware Bazaar, etc.
- **Pros**: Controle total, atual
- **Contras**: Trabalhoso, questões éticas/legais

## Formato Esperado

### Para Baseline (ML Clássico)
```
features.csv:
md5,family,feature1,feature2,...,feature2381
abc123,Trojan.Generic,0.42,1.5,...,0.88
```

### Para CNN (Imagens)
```
images/
├── train/
│   ├── family1/
│   │   ├── sample1.png
│   │   ├── sample2.png
│   └── family2/
│       ├── sample1.png
├── val/
│   └── ...
└── test/
    └── ...
```

## Entregáveis

1. **dataset-info.md**: Documentação completa
2. **eda.ipynb**: Análise exploratória com gráficos
3. **splits/**: Arquivos train.txt, val.txt, test.txt com listas
4. **statistics.md**: Estatísticas descritivas
5. **samples/**: Amostras de exemplo (se possível compartilhar)

## Próximo Experimento

➡️ [01-binary-to-image](../01-binary-to-image/) - Conversão de binários para imagens (se necessário)
