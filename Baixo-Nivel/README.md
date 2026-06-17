# Baixo-Nível: Arquitetura e Engenharia Reversa

## Visão Geral

Estudos de fundamentos em baixo-nível essenciais para análise e engenharia reversa de malware. Conhecimento de Assembly, arquitetura de processadores e estruturas de executáveis é crítico para:

1. **Análise Estática Avançada:** Entender disassembly sem depender do decompiler
2. **Validação de Resultados:** Verificar manualmente classificações do modelo
3. **Feature Engineering:** Extrair características (CFG, API calls, entropy)
4. **Profundidade Técnica:** Tsukuba valoriza compreensão real, não apenas uso de frameworks

---

## Conteúdo

### [OST2-Architecture-1001/](OST2-Architecture-1001/)
Curso de arquitetura x86/x64 e Assembly
- Registradores, flags, instruções básicas
- Stack frames, calling conventions
- Interação Assembly ↔ C/C++

#### [Crackmes/](OST2-Architecture-1001/Crackmes/)
Exercícios práticos de reversing (iniciante → avançado)
- Comparação de strings (strcmp)
- Algoritmos de checksum (MD5, CRC)
- Anti-debugging e obfuscação

---

## Objetivos de Aprendizado

### Conhecimentos Fundamentais
- [x] **Arquitetura x86/x64:** Diferenças entre 32-bit e 64-bit (calling convention, registradores estendidos)
- [ ] **Assembly (NASM/GAS):** Leitura fluente de disassembly em sintaxe Intel e AT&T
- [ ] **Estrutura de Executáveis:**
  - PE (Windows): Headers, sections (.text, .data, .rdata), Import/Export tables
  - ELF (Linux): ELF headers, segments, GOT/PLT
- [ ] **Debugging:** Breakpoints, step-over/into, memory inspection, register modification
- [ ] **Obfuscação:** Reconhecer opaque predicates, control-flow flattening, packing (UPX)

### Habilidades Práticas
- [ ] Analisar binário desconhecido e identificar função principal (main)
- [ ] Reverter algoritmo de checksum simples (XOR, MD5)
- [ ] Modificar executável para bypass de validação (patching)
- [ ] Extrair CFG (Control Flow Graph) de função com Ghidra Script
- [ ] Desempacotar malware básico (UPX, packers genéricos)

---

## Ferramentas Essenciais

### Análise Estática
- **Ghidra** (NSA) - Disassembler/decompiler open-source [preferido para TCC]
- **IDA Pro** (Free/Pro) - Padrão da indústria, scripting em Python/IDC
- **Binary Ninja** - Interface moderna, API excelente
- **radare2** - CLI-based, poderoso para automação

### Análise Dinâmica
- **x64dbg** (Windows) - Sucessor do OllyDbg, plugins ativos
- **GDB + GEF/pwndbg** (Linux) - Debugger scriptável
- **WinDbg** (Windows) - Kernel-mode debugging
- **Frida** - Dynamic instrumentation (hook functions em runtime)

### Utilitários
- **PE-bear** - Visualizar estrutura PE graficamente
- **PEiD** - Detectar packers/compiladores
- **Detect It Easy (DIE)** - Alternativa moderna ao PEiD
- **strings** - Extrair strings legíveis de binários

---

## Tópicos Avançados

### Para Integração com o TCC
1. **Extração de Features Estáticas:**
   - API calls frequency (GetProcAddress, VirtualAlloc, CreateProcess)
   - Entropy por seção (packed sections têm entropy alta)
   - Ratio de instruções (MOV/CALL/JMP) para identificar código vs dados
   
2. **Control Flow Graph (CFG):**
   - Extrair com Ghidra API ou radare2
   - Representar como grafo para Graph Neural Networks (GNN)
   - Comparar similaridade de CFGs entre famílias

3. **Desofuscação Automática:**
   - Executar emulação com Unicorn Engine
   - Desempacotar dinamicamente em sandbox

---

## Recursos de Aprendizado

### Cursos Online
- **OpenSecurityTraining:** "Introduction to Reverse Engineering" (Xeno Kovah)
- **Malware Unicorn:** Workshops gratuitos de RE
- **pwn.college:** Curso da ASU sobre binary exploitation

### Livros Essenciais
1. **"Practical Malware Analysis" - Sikorski & Honig** ⭐ Capítulos 1-9
2. **"Practical Binary Analysis" - Dennis Andriesse** (foco em tooling)
3. **"Reversing: Secrets of Reverse Engineering" - Eldad Eilam** (clássico)
4. **"The Art of Assembly Language" - Randall Hyde** (fundamentos)

### Papers Acadêmicos
- **Saxe & Berlin (2015)** - "Deep Neural Network Based Malware Detection Using Two Dimensional Binary Program Features"
- **Gibert et al. (2020)** - "Using Convolutional Neural Networks for Classification of Malware Represented as Images"

---

## Exercícios Progressivos

### Fase 1: Reconhecimento (Semana 1-2)
- [ ] Identificar compilador/linguagem de 10 binários (C, C++, Go, Rust, Python compiled)
- [ ] Extrair todas as strings e imports de um malware sample
- [ ] Desenhar manualmente o CFG de uma função simples (30-50 instruções)

### Fase 2: Análise (Semana 3-4)
- [ ] Resolver 5 crackmes de nível iniciante
- [ ] Analisar estaticamente um sample de malware real (não executar!)
- [ ] Desempacotar UPX manualmente (sem usar `upx -d`)

### Fase 3: Automação (Semana 5-6)
- [ ] Escrever Ghidra script Python para extrair todas as API calls
- [ ] Implementar extrator de features PE em Python (usando `pefile` lib)
- [ ] Gerar CFG visual de um binário usando r2pipe + Graphviz

---

## Conexão com Mestrado

### Mestrados de ponta exigem profundidade

Tsukuba valoriza pesquisadores que entendem o funcionamento interno dos modelos. Publicar em conferências (IEEE S&P, NDSS, USENIX Security) requer validação técnica rigorosa. Professores como Prof. Koshiba (cryptography) e Prof. Miyamoto (software security) esperam fluência em análise de baixo-nível.

**Diferencial:**
- Maioria dos projetos de ML em malware são black-box (dataset → CNN → resultados)
- Trabalhos relevantes combinam ML com análise qualitativa
- Exemplo: Grad-CAM mostra CNN focando em seção .text → validar manualmente com IDA que aquela região contém payload característico da família

---

## Critérios de Proficiência

Você está pronto para integrar este conhecimento ao TCC quando conseguir:

1. ✅ Abrir um malware desconhecido no Ghidra e identificar main/WinMain em < 5 min
2. ✅ Explicar o que cada linha de Assembly faz em uma função de 50 linhas
3. ✅ Escrever script Python que extrai lista de API calls de um PE
4. ✅ Identificar técnicas de evasão (anti-VM, anti-debug) no disassembly
5. ✅ Comparar manualmente 2 samples e dizer se são da mesma família (sem ML)

**Próximo:** Aplicar essas habilidades para validar as predições do seu modelo de CNN!

---

## Progresso

**Status:** Em andamento (OST2-Architecture-1001)
**Próximos Passos:**
1. Completar módulos de OST2-Architecture-1001
2. Resolver 10 crackmes (5 iniciante, 3 intermediário, 2 avançado)
3. Analisar 3 samples de malware real (WannaCry, Emotet, TrickBot) estaticamente
4. Implementar extrator de features PE para o TCC
