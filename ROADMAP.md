# Roadmap do TCC

## Objetivo
Desenvolver um sistema de classificação de famílias de malware usando Deep Learning, representação visual de binários e análise estática.

## Fase 1: Fundamentos (Em Andamento)

### Baixo Nível
- [ ] Concluir OST2-Architecture-1001
- [O] Estudar Assembly x86/x64 (NASM, GDB)
- [ ] Praticar engenharia reversa com crackmes
- [ ] Consolidar conhecimento em `02-fundamentos/baixo-nivel/`

### IA e Dados
- [O] Concluir Python for Data Science and ML
- [ ] Estudar PyTorch for Deep Learning
- [ ] Praticar CNNs e Computer Vision
- [ ] Consolidar conhecimento em `02-fundamentos/ia-e-dados/`

## Fase 2: Revisão Bibliográfica (A Iniciar)

- [ ] Fichamento de 10-15 papers chave
- [ ] Criar matriz de comparação de abordagens
- [ ] Documentar perguntas em aberto
- [ ] Identificar gaps e oportunidades

## Fase 3: Laboratórios Práticos (A Iniciar)

- [ ] Extrair features de binários (PE, ELF)
- [ ] Converter binários para imagens
- [ ] Praticar análise estática com Ghidra
- [ ] Criar scripts de automação

## Fase 4: Experimentos do TCC (A Iniciar)

### 00-dataset
- [ ] Definir dataset público
- [ ] Documentar processo de coleta
- [ ] Preparar splits (train/val/test)

### 01-binary-to-image
- [ ] Implementar conversão binário → imagem
- [ ] Testar diferentes tamanhos e formatos
- [ ] Visualizar amostras

### 02-baseline-ml-classico
- [ ] Extrair features clássicas
- [ ] Treinar Random Forest, SVM
- [ ] Estabelecer baseline de performance

### 03-cnn-pytorch
- [ ] Implementar arquitetura CNN
- [ ] Treinar e validar modelo
- [ ] Comparar com baseline

### 04-gradcam-xai
- [ ] Implementar Grad-CAM
- [ ] Visualizar regiões importantes
- [ ] Interpretar resultados

### 05-resultados
- [ ] Consolidar métricas
- [ ] Criar visualizações
- [ ] Documentar conclusões

## Fase 5: Escrita do TCC (A Iniciar)

- [ ] Proposta inicial
- [ ] Fundamentação teórica
- [ ] Metodologia
- [ ] Resultados e discussão
- [ ] Conclusão e trabalhos futuros

## Milestones

| Data | Milestone |
|------|-----------|
| Jul 2026 | Fundamentos concluídos |
| Ago 2026 | Revisão bibliográfica completa |
| Set 2026 | Laboratórios práticos finalizados |
| Out 2026 | Experimentos baseline |
| Nov 2026 | Experimentos CNN finalizados |
| Dez 2026 | Proposta TCC submetida |
| Jan 2027 | XAI e análise |
| Fev 2027 | Escrita TCC |
| Mar 2027 | Revisão e defesa |

## Próximos Passos Imediatos

1. Concluir notebooks de Python básico
2. Resolver 3 crackmes iniciantes
3. Fichar 2 papers principais
4. Criar primeiro protótipo de conversão binário → imagem
