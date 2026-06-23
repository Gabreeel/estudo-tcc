# assets

Recursos visuais e multimídia do projeto.

## Estrutura

### images/
Imagens gerais do projeto:
- **diagrams/**: Diagramas de arquitetura, pipelines, fluxogramas
- **screenshots/**: Capturas de tela de ferramentas, resultados
- **logos/**: Logos de instituições, frameworks, ferramentas
- **examples/**: Exemplos visuais de conceitos

### plots/
Gráficos e visualizações:
- **exploratory/**: Gráficos de análise exploratória
- **results/**: Gráficos de resultados de experimentos
- **comparisons/**: Comparações entre abordagens
- **heatmaps/**: Grad-CAM e outras visualizações de XAI

### videos/
Vídeos e gravações:
- **demos/**: Demonstrações de ferramentas ou resultados
- **presentations/**: Gravações de apresentações
- **tutorials/**: Tutoriais criados

### documents/
Documentos auxiliares:
- PDFs de referência
- Datasheets
- Especificações técnicas

## Convenções de Nomenclatura

### Imagens
```
categoria-descricao-versao.extensao
```
Exemplo: `diagram-pipeline-tcc-v2.png`

### Plots
```
experimento-metrica-formato.extensao
```
Exemplo: `baseline-confusion-matrix.png`

### Vídeos
```
YYYY-MM-DD-tipo-descricao.extensao
```
Exemplo: `2026-09-15-demo-binary-to-image.mp4`

## Formatos Recomendados

### Imagens Estáticas
- **PNG**: Diagramas, screenshots, plots (melhor qualidade)
- **JPG**: Fotos, imagens fotográficas (menor tamanho)
- **SVG**: Diagramas vetoriais (escaláveis, ideais para LaTeX)

### Gráficos
- **PNG**: Para apresentações e documentos
- **SVG/PDF**: Para LaTeX (melhor qualidade)
- **EPS**: Para publicações acadêmicas (se necessário)

### Vídeos
- **MP4**: Compatibilidade universal
- **GIF**: Animações curtas

## Geração de Figuras

### Matplotlib/Seaborn
```python
import matplotlib.pyplot as plt
import seaborn as sns

# Configurar estilo
sns.set_style("whitegrid")
plt.rcParams['figure.figsize'] = (10, 6)
plt.rcParams['font.size'] = 12

# Criar gráfico
fig, ax = plt.subplots()
# ... plotar ...

# Salvar em múltiplos formatos
fig.savefig('assets/plots/experimento-metrica.png', dpi=300, bbox_inches='tight')
fig.savefig('assets/plots/experimento-metrica.pdf', bbox_inches='tight')
```

### Draw.io
- Usar para diagramas de arquitetura
- Exportar como PNG (apresentações) e SVG (LaTeX)
- Manter arquivo fonte `.drawio` versionado

### TikZ (LaTeX)
- Para diagramas acadêmicos de alta qualidade
- Manter código `.tex` em `assets/images/diagrams/source/`

## Organização

### Por Experimento
```
plots/
├── baseline/
│   ├── confusion-matrix.png
│   ├── roc-curve.png
│   └── feature-importance.png
├── cnn/
│   ├── training-loss.png
│   ├── validation-accuracy.png
│   └── confusion-matrix.png
└── xai/
    ├── gradcam-sample-1.png
    ├── gradcam-sample-2.png
    └── attention-maps.png
```

### Por Tipo
```
images/
├── diagrams/
│   ├── pipeline-geral.svg
│   ├── arquitetura-cnn.svg
│   └── processo-conversao.svg
├── screenshots/
│   ├── ghidra-analysis.png
│   └── binary-visualization.png
└── examples/
    ├── pe-structure.png
    └── malware-families.png
```

## Uso no TCC

### Em Markdown
```markdown
![Descrição da figura](../assets/plots/baseline/confusion-matrix.png)

*Figura 1: Matriz de confusão do baseline com Random Forest.*
```

### Em LaTeX
```latex
\begin{figure}[htb]
    \centering
    \includegraphics[width=0.8\textwidth]{assets/plots/baseline/confusion-matrix.pdf}
    \caption{Matriz de confusão do baseline com Random Forest.}
    \label{fig:baseline-confusion}
\end{figure}
```

### Em Notebooks
```python
from IPython.display import Image, display

# Mostrar imagem
display(Image('../assets/images/examples/pe-structure.png'))

# Ou com matplotlib
import matplotlib.pyplot as plt
import matplotlib.image as mpimg

img = mpimg.imread('../assets/plots/cnn/training-loss.png')
plt.imshow(img)
plt.axis('off')
plt.show()
```

## Dicas

1. **Alta Resolução**: Salve plots com DPI 300 ou superior
2. **Vetorial quando possível**: SVG/PDF para gráficos escaláveis
3. **Consistência visual**: Use mesma paleta de cores
4. **Legendas claras**: Toda figura deve ter legenda descritiva
5. **Versionamento**: Mantenha versões antigas com sufixo `-v1`, `-v2`
6. **Tamanho**: Otimize imagens grandes (use ferramentas de compressão)

## .gitignore para Assets

Alguns assets não devem ser versionados:
- Vídeos muito grandes (> 50MB)
- Datasets de imagens completos
- Arquivos temporários de edição

Adicionar ao `.gitignore`:
```
assets/videos/**/*.mp4
assets/plots/raw/
assets/.tmp/
```
