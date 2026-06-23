# notebooks

Jupyter notebooks para exploração, prototipagem e documentação interativa.

## Estrutura

### exploratorios/
Notebooks de exploração inicial:
- Análise exploratória de datasets
- Testes rápidos de ideias
- Visualizações ad-hoc
- Debugging interativo

**Característica**: Podem estar "bagunçados", servem para experimentar.

### prototipos/
Notebooks de prototipagem:
- Protótipos de modelos
- Testes de arquiteturas
- Pipelines experimentais
- Validação de abordagens

**Característica**: Mais organizados que exploratórios, mas ainda não finais.

### finais/
Notebooks polidos para apresentação:
- Demonstrações completas
- Análises finais
- Visualizações para TCC
- Reprodução de experimentos

**Característica**: Limpos, bem documentados, prontos para compartilhar.

## Convenções de Nomenclatura

### Exploratórios
```
YYYY-MM-DD-descrição-curta.ipynb
```
Exemplo: `2026-06-19-analise-dataset-ember.ipynb`

### Protótipos
```
v01-nome-do-prototipo.ipynb
v02-nome-do-prototipo.ipynb
```
Exemplo: `v01-cnn-baseline.ipynb`

### Finais
```
final-topico-descricao.ipynb
```
Exemplo: `final-binary-to-image-conversion.ipynb`

## Boas Práticas

### 1. Organização
- Células de markdown para documentar
- Seções claras com headers
- Sumário no início para notebooks longos

### 2. Código Limpo
```python
# Importações no topo, organizadas
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

# Configurações globais
%matplotlib inline
plt.style.use('seaborn-v0_8')
np.random.seed(42)

# Código modular
def load_data(path):
    """Carrega dados do caminho especificado."""
    return pd.read_csv(path)
```

### 3. Visualizações
- Títulos claros
- Legendas descritivas
- Tamanho adequado (figsize)
- Salvar figuras importantes

### 4. Resultados
- Documentar decisões
- Capturar outputs importantes
- Explicar por que algo funcionou ou não

## Exemplos de Notebooks

### Exploratório Típico
```markdown
# Análise Exploratória: Dataset EMBER

**Data**: 2026-06-19  
**Objetivo**: Entender distribuição de classes e features

## 1. Carregamento dos Dados
## 2. Estatísticas Descritivas
## 3. Visualizações
## 4. Insights e Próximos Passos
```

### Protótipo Típico
```markdown
# Protótipo v01: CNN Baseline

**Data**: 2026-07-15  
**Objetivo**: Testar arquitetura CNN simples

## 1. Setup e Configuração
## 2. Carregamento de Dados
## 3. Definição do Modelo
## 4. Treino
## 5. Avaliação
## 6. Conclusões e Próximas Iterações
```

### Final Típico
```markdown
# Conversão de Binários para Imagens

**Autor**: [Seu Nome]  
**Data**: 2026-08-20  
**Versão**: 1.0

## Resumo
Este notebook demonstra o processo completo de conversão...

## 1. Introdução
## 2. Metodologia
## 3. Implementação
## 4. Resultados
## 5. Discussão
## 6. Conclusões
## 7. Referências
```

## Dicas

1. **Execute tudo antes de commitar**: Cell → Run All
2. **Limpe outputs grandes**: Clear Output antes de commitar
3. **Use checkpoints**: Salve modelos/dados intermediários
4. **Versionamento**: Git funciona bem com notebooks limpos
5. **Documentação**: Notebooks finais são parte da documentação do TCC

## Conversão para Scripts

Notebooks exploratórios/protótipos que funcionam bem podem virar scripts em `src/`:

```bash
# Converter notebook para script Python
jupyter nbconvert --to script notebook.ipynb

# Ou usar ferramenta como nb2py
```

## Integração com Experimentos

Notebooks em `finais/` devem referenciar código de `src/` e experimentos de `05-experimentos-tcc/`:

```python
# Importar código reutilizável
from malware_tcc.preprocessing import binary_parser
from malware_tcc.models import cnn_baseline

# Carregar resultados de experimentos
results = pd.read_csv('../05-experimentos-tcc/05-resultados/metrics.csv')
```
