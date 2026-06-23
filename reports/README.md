# reports

Documentos formais, apresentações e relatórios do TCC.

## Estrutura

### proposta-tcc/
Proposta inicial do trabalho:
- **proposta-completa.md**: Documento completo da proposta
- **resumo-executivo.md**: Resumo de 1-2 páginas
- **slides-apresentacao.pdf**: Slides para defesa de proposta
- **cronograma-detalhado.md**: Timeline do projeto

### apresentacoes/
Apresentações durante o desenvolvimento:
- **seminario-1-fundamentos.pdf**: Apresentação de fundamentos
- **seminario-2-revisao-bibliografica.pdf**: Revisão da literatura
- **seminario-3-metodologia.pdf**: Metodologia e experimentos
- **seminario-4-resultados-preliminares.pdf**: Primeiros resultados

### relatorio-final/
TCC final completo:
- **tcc-completo.tex**: Documento LaTeX principal
- **chapters/**: Capítulos individuais
  - `01-introducao.tex`
  - `02-fundamentacao.tex`
  - `03-trabalhos-relacionados.tex`
  - `04-metodologia.tex`
  - `05-experimentos.tex`
  - `06-resultados.tex`
  - `07-conclusao.tex`
- **figures/**: Figuras do documento
- **tables/**: Tabelas do documento
- **references.bib**: Bibliografia BibTeX

## Formato da Proposta

### Estrutura Sugerida

1. **Introdução** (1-2 páginas)
   - Contexto e motivação
   - Problema
   - Objetivos
   
2. **Fundamentação Teórica** (2-3 páginas)
   - Análise de malware
   - Deep Learning e CNNs
   - Trabalhos relacionados (resumo)

3. **Metodologia Proposta** (2-3 páginas)
   - Dataset
   - Representação visual de binários
   - Arquitetura CNN
   - Pipeline de experimentos
   - Métricas de avaliação

4. **Cronograma** (1 página)
   - Timeline de atividades
   - Milestones
   - Entregáveis

5. **Referências** (1-2 páginas)
   - Papers principais
   - Ferramentas e frameworks

**Total**: 8-12 páginas

## Formato do TCC Final

### Estrutura Sugerida (ABNT)

1. **Elementos Pré-Textuais**
   - Capa
   - Folha de rosto
   - Resumo (PT)
   - Abstract (EN)
   - Sumário

2. **Introdução** (3-5 páginas)
   - Contexto
   - Motivação
   - Problema de pesquisa
   - Objetivos (geral e específicos)
   - Contribuições
   - Organização do trabalho

3. **Fundamentação Teórica** (10-15 páginas)
   - Análise de malware (estática, dinâmica, famílias)
   - Machine Learning clássico
   - Deep Learning e CNNs
   - Computer Vision para segurança
   - Explainable AI (XAI)

4. **Trabalhos Relacionados** (8-12 páginas)
   - Revisão sistemática
   - Comparação de abordagens
   - Análise crítica
   - Posicionamento do trabalho

5. **Metodologia** (8-12 páginas)
   - Dataset (coleta, preparação, análise)
   - Representação visual de binários
   - Extração de features (baseline)
   - Arquitetura CNN proposta
   - Pipeline de treinamento
   - Métricas e validação
   - Técnicas de XAI

6. **Experimentos e Resultados** (12-18 páginas)
   - Configuração experimental
   - Baseline (ML clássico)
   - CNN e variações
   - Análise de resultados
   - Visualizações XAI
   - Discussão

7. **Conclusão** (3-5 páginas)
   - Síntese dos resultados
   - Contribuições alcançadas
   - Limitações
   - Trabalhos futuros

8. **Elementos Pós-Textuais**
   - Referências
   - Apêndices (código, configs, etc.)

**Total**: 50-80 páginas (dependendo do formato da instituição)

## Templates LaTeX

### Overleaf
- Template ABNT para TCC
- Template IEEE (se aplicável)
- Template ACM (para artigos)

### Locais
Manter versão LaTeX em `relatorio-final/` para controle de versão.

## Ferramentas

### Escrita
- **Overleaf**: Editor LaTeX online colaborativo
- **VS Code + LaTeX Workshop**: Editor local
- **Grammarly**: Revisão gramatical (inglês)
- **Zotero/Mendeley**: Gerenciamento de referências

### Apresentações
- **PowerPoint/Google Slides**: Apresentações tradicionais
- **LaTeX Beamer**: Apresentações acadêmicas
- **reveal.js**: Apresentações web interativas

### Figuras
- **draw.io**: Diagramas e fluxogramas
- **TikZ**: Figuras LaTeX vetoriais
- **matplotlib/seaborn**: Gráficos de resultados
- **Inkscape**: Edição vetorial

## Dicas de Escrita

1. **Clareza**: Escreva de forma clara e direta
2. **Objetividade**: Evite jargões desnecessários
3. **Estrutura**: Siga estrutura lógica e progressiva
4. **Figuras**: Uma boa figura vale mais que mil palavras
5. **Resultados**: Apresente resultados honestamente (incluindo limitações)
6. **Revisão**: Revise múltiplas vezes, peça feedback

## Cronograma de Escrita

1. **Proposta**: 2-3 semanas para elaborar e revisar
2. **Capítulos iniciais** (durante experimentos):
   - Introdução: enquanto faz revisão bibliográfica
   - Fundamentação: conforme consolida conhecimento
   - Trabalhos relacionados: após fichar papers
3. **Capítulos finais** (após experimentos):
   - Metodologia: 1-2 semanas
   - Resultados: 2-3 semanas
   - Conclusão: 1 semana
4. **Revisão final**: 2-3 semanas
5. **Apresentação**: 1 semana de preparação

**Total**: 3-4 meses de escrita (paralelo aos experimentos)
