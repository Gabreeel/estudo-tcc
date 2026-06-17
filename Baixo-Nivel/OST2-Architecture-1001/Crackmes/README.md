# Crackmes - Exercícios de Engenharia Reversa

## O que são Crackmes?

Crackmes são pequenos programas desafio criados para praticar engenharia reversa. O objetivo típico é:
- Encontrar a senha/chave correta sem ter acesso ao código-fonte
- Modificar o executável para bypass de verificações (patching)
- Entender algoritmos de validação e criptografia simples

**Importante:** Crackmes são exercícios legais e educacionais, diferentes de cracking comercial (ilegal).

---

## Objetivos Pedagógicos

### Habilidades Desenvolvidas
1. **Leitura de Assembly:** Interpretar disassembly do Ghidra/IDA
2. **Debugging Dinâmico:** Usar breakpoints, step-over, watch de memória
3. **Análise de Strings:** Identificar mensagens de sucesso/erro como pontos de referência
4. **Identificação de Funções:** Reconhecer strcmp, strlen, MD5, etc.
5. **Patching:** Modificar bytes para inverter lógica (JE → JNE)

### Relevância para Análise de Malware
- **Detecção de Anti-debug:** Crackmes ensinam técnicas usadas por malware (IsDebuggerPresent, PEB checks)
- **Desofuscação:** Entender loops e transformações aplicadas a strings/chaves
- **Análise de Controle de Fluxo:** Seguir ramificações para encontrar código crítico

---

## Estrutura

```
Crackmes/
├── iniciante/         # Crackmes nível 1-2 (strcmp simples)
├── intermediario/     # Crackmes nível 3-4 (XOR, checksums)
├── avancado/          # Crackmes nível 5+ (anti-debug, VM detection)
├── writeups/          # Soluções documentadas (criar após resolver)
└── README.md          # Este arquivo
```

---

## Ferramentas Recomendadas

### Análise Estática
- **Ghidra:** Disassembler + decompiler gratuito (NSA)
- **IDA Free:** Versão gratuita limitada a x86/x64
- **Binary Ninja:** Alternativa moderna (trial disponível)
- **strings:** Ferramenta Linux para extrair strings legíveis

### Análise Dinâmica
- **x64dbg:** Debugger para Windows (sucessor do OllyDbg)
- **GDB + GEF/pwndbg:** Debugging no Linux com plugins
- **Frida:** Instrumentação dinâmica (avançado)

### Patching
- **HxD / 010 Editor:** Hex editors para modificar bytes
- **Ghidra Script:** Automatizar patches com Python

---

## Níveis de Dificuldade

### Iniciante (Nível 1-2)
**Foco:** Comparação simples de strings
- Buscar por `strcmp`, `strncmp` no disassembly
- Encontrar string hardcoded no binário
- **Exemplo:** `if (input == "secret123") → success()`

**Primeiros Passos:**
1. Rodar `strings crackme.exe` para ver strings visíveis
2. Abrir no Ghidra e procurar por `main`
3. Identificar chamada a `strcmp` ou `scanf`
4. Ler argumentos da comparação

### Intermediário (Nível 3-4)
**Foco:** Algoritmos de validação (checksum, XOR, base64)
- Chave não está hardcoded, mas é calculada
- Necessário entender o algoritmo de verificação
- **Exemplo:** `if (md5(input) == "5f4dcc3b5...") → success()`

**Abordagem:**
1. Identificar loops suspeitos (possível checksum)
2. Anotar operações aplicadas ao input
3. Reverter o algoritmo ou bruteforce

### Avançado (Nível 5+)
**Foco:** Anti-debugging, obfuscação, VM detection
- Detecta se está sendo debuggado (IsDebuggerPresent, RDTSC)
- Código ofuscado com opaque predicates
- **Exemplo:** VM que interpreta bytecode customizado

**Técnicas Necessárias:**
- Patching de anti-debug checks
- Dumping de memória após desofuscação
- Scripting com Ghidra/Binary Ninja

---

## Onde Encontrar Crackmes

### Sites Oficiais
- **[Crackmes.one](https://crackmes.one/)** - Repositório moderno e ativo
- **[Root-me Cracking Challenges](https://www.root-me.org/?page=challenges&lang=en)** - CTF-style
- **[RingZer0 Team](https://ringzer0ctf.com/)** - Cracking section

### Recomendados para Iniciantes
1. **"KeygenMe" by Mr.dD** (Windows, strcmp simples)
2. **"Simple CrackMe" by Ricardo Narvaja** (série didática)
3. **Crackmes da série "Lenas Reversing for Newbies"**

---

## Template de Writeup

Ao resolver um crackme, documente em `writeups/nome-do-crackme.md`:

```markdown
# [Nome do Crackme] - Writeup

**Dificuldade:** [Iniciante/Intermediário/Avançado]  
**Plataforma:** [Windows/Linux/macOS]  
**Ferramentas:** [Ghidra, x64dbg, etc.]

## Objetivo
[Descrever o que o crackme pede]

## Análise Estática
[Observações do disassembly]

## Análise Dinâmica
[Debugging, breakpoints importantes]

## Solução
[Chave/flag encontrada ou patch aplicado]

## Lições Aprendidas
[Conceitos de Assembly ou reversing aprendidos]
```

---

## Progresso

| Crackme | Nível | Status | Writeup |
|---------|-------|--------|---------|
| -       | -     | Não iniciado | - |

---

## Recursos de Aprendizado

### Tutoriais Clássicos
- **"Lenas Reversing for Newbies"** - Série de tutoriais em vídeo/texto
- **OpenSecurityTraining:** Curso "Introduction to Reverse Engineering"
- **Nightmare (CTF):** [guyinatuxedo/nightmare](https://guyinatuxedo.github.io/)

### Livros
- **"Practical Malware Analysis" - Sikorski & Honig** (Capítulos 1-5)
- **"Reversing: Secrets of Reverse Engineering" - Eldad Eilam**

---

## Aviso Legal

**Crackmes são para fins educacionais.** Nunca aplique essas técnicas em software comercial sem permissão explícita. Cracking de software proprietário é ilegal na maioria das jurisdições.
