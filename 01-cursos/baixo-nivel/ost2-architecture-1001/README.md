# OST2-Architecture-1001

## Sobre o Curso

Curso de arquitetura de computadores focado em x86/x64, Assembly e fundamentos de baixo-nível para engenharia reversa de malware.

## Objetivos de Aprendizado

### Conhecimentos-Chave
- **Arquitetura x86/x64:** Registradores (RAX, RBX, RCX, RDX, RSI, RDI, RSP, RBP), modos de endereçamento
- **Assembly (NASM/GAS):** Sintaxe Intel vs AT&T, instruções básicas (MOV, ADD, SUB, CMP, JMP, CALL, RET)
- **Stack & Calling Conventions:** cdecl, stdcall, fastcall, x64 calling convention (System V vs Microsoft)
- **Estruturas de Dados:** Arrays, structs, ponteiros em baixo-nível
- **Interação com C/C++:** Como o compilador traduz código de alto-nível

### Relevância para Análise de Malware
- **Leitura de Disassembly:** Entender output do Ghidra/IDA sem confusão
- **Identificação de Padrões:** Reconhecer loops, condicionais, funções obfuscadas
- **Unpacking Manual:** Seguir fluxo de execução de packers (UPX, Themida)
- **Análise de Exploits:** Compreender buffer overflows, ROP chains, shellcode

---

## Estrutura do Material

```
OST2-Architecture-1001/
├── Crackmes/          # Exercícios práticos de reversing
├── notas/             # Anotações de aulas (a criar)
├── exercicios/        # Códigos Assembly de estudo (a criar)
└── README.md          # Este arquivo
```

---

## Ferramentas Utilizadas

### Assembladores e Debuggers
- **NASM:** Assembler para sintaxe Intel
- **GDB/LLDB:** Debugging em Linux/macOS
- **x64dbg:** Debugger moderno para Windows
- **WinDbg:** Debugger oficial da Microsoft

### Disassemblers
- **Ghidra:** Ferramenta open-source da NSA (preferida para o TCC)
- **IDA Pro:** Padrão da indústria (versão Free disponível)
- **Binary Ninja:** Alternativa moderna

---

## Tópicos Estudados

### Módulo 1: Fundamentos
- [ ] Arquitetura Von Neumann
- [ ] Registradores de propósito geral (x86 vs x64)
- [ ] Flags (ZF, CF, SF, OF, PF)
- [ ] Segmentação de memória (CS, DS, SS, ES)

### Módulo 2: Assembly Básico
- [ ] Instruções aritméticas (ADD, SUB, MUL, DIV, INC, DEC)
- [ ] Instruções lógicas (AND, OR, XOR, NOT, SHL, SHR)
- [ ] Movimentação de dados (MOV, LEA, PUSH, POP)
- [ ] Controle de fluxo (JMP, JE, JNE, JG, JL, CALL, RET)

### Módulo 3: Stack e Funções
- [ ] Stack frames e base pointer (EBP/RBP)
- [ ] Prólogo e epílogo de funções
- [ ] Passagem de argumentos (stack vs registradores)
- [ ] Retorno de valores

### Módulo 4: Tópicos Avançados
- [ ] Syscalls (int 0x80, syscall)
- [ ] Inline assembly em C
- [ ] SIMD (SSE, AVX) - básico
- [ ] Interações com heap (malloc/free em Assembly)

---

## Exercícios Práticos

Ver pasta [Crackmes/](Crackmes/) para desafios de reversing progressivos.

---

## Recursos Adicionais

### Livros
- **"Programming from the Ground Up" - Jonathan Bartlett**
- **"Practical Reverse Engineering" - Bruce Dang et al.**
- **"The Art of Assembly Language" - Randall Hyde**

### Tutoriais Online
- [x86 Assembly Guide (University of Virginia)](http://www.cs.virginia.edu/~evans/cs216/guides/x86.html)
- [Compiler Explorer (Godbolt)](https://godbolt.org/) - Veja como C vira Assembly
- [OSdev Wiki](https://wiki.osdev.org/) - Detalhes de arquitetura

### Cheatsheets
- [x86 Opcode Reference](http://ref.x86asm.net/)
- [Calling Conventions](https://en.wikipedia.org/wiki/X86_calling_conventions)

---

## Progresso Atual

**Status:** Em andamento  
**Próximo:** Completar módulos de controle de fluxo e funções
