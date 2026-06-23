# 04-laboratorios

Prática hands-on de conceitos técnicos. Labs são exercícios estruturados para desenvolver habilidades práticas necessárias ao TCC.

## Estrutura

### crackmes/
Desafios de engenharia reversa para praticar:
- **iniciante/**: Crackmes simples
- **intermediario/**: Crackmes com obfuscação
- **avancado/**: Crackmes complexos
- **writeups/**: Soluções documentadas

### ghidra-scripts/
Scripts Python para automação no Ghidra:
- Extração de strings
- Análise de imports
- Detecção de padrões
- Exportação de features

### assembly-exercicios/
Exercícios práticos de Assembly:
- Escrita de funções básicas
- Manipulação de stack
- Syscalls
- Debugging com GDB

### feature-extraction/
Laboratórios de extração de features:
- Features estáticas de PE/ELF
- N-grams de bytes
- Imports e exports
- Seções e entropy

## Objetivo

Desenvolver **habilidades práticas** necessárias para:
1. Analisar binários estaticamente
2. Extrair features relevantes
3. Automatizar análises
4. Validar conceitos dos cursos

## Progressão Sugerida

1. **Semana 1-2**: 3-5 crackmes iniciantes
2. **Semana 3-4**: Ghidra básico + 1 script simples
3. **Semana 5-6**: Assembly exercícios + debugging
4. **Semana 7-8**: Feature extraction + automação

## Uso dos Templates

Documente cada lab usando [template-lab.md](../templates/template-lab.md):
- Objetivo claro
- Passos reproduzíveis
- Capturas de tela
- Lições aprendidas
- Conexão com TCC

## Recursos

### Crackmes
- **crackmes.one**: https://crackmes.one/
- **Reversing.kr**: http://reversing.kr/
- **CTFTime**: https://ctftime.org/

### Ghidra
- **Documentação**: https://ghidra-sre.org/
- **Ghidra Scripts**: https://github.com/topics/ghidra-scripts
- **Tutoriais**: OALabs, YouTube

### Assembly
- **GDB Tutorial**: https://sourceware.org/gdb/documentation/
- **Assembly Challenges**: pwnable.kr, overthewire

## Conexão com TCC

Cada lab deve conectar-se diretamente com alguma parte do TCC:
- **Crackmes** → entender estrutura de binários
- **Ghidra scripts** → automatizar feature extraction
- **Assembly** → fundamentar análise estática
- **Feature extraction** → preparar pipeline do experimento
