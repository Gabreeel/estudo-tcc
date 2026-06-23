# baixo-nivel

Cursos de fundamentos de baixo nível: arquitetura, assembly, engenharia reversa.

## Cursos

### ost2-architecture-1001
**Status**: 🟢 Em Progresso  
**Fonte**: OpenSecurityTraining2  
**Descrição**: Fundamentos de arquitetura x86/x64, registradores, memória, instruções

**Progresso**: 12/50 módulos  
**Aplicação no TCC**: Entender estrutura de binários executáveis

📁 [Ver pasta](./ost2-architecture-1001/)

### udemy-x86-64-assembly
**Status**: ⚪ Planejado  
**Fonte**: Udemy  
**Descrição**: Assembly x86/x64, NASM, GDB, debugging prático

**Progresso**: 0/80 aulas  
**Aplicação no TCC**: Análise estática de binários, compreensão de comportamento

📁 [Ver pasta](./udemy-x86-64-assembly/)

## Próximos Cursos

- **Ghidra for Reverse Engineering**: Automação de análise estática
- **IDA Pro Advanced**: Análise avançada de malware

## Conexão com TCC

Conhecimento de baixo nível é essencial para:
1. **Extração de features estáticas**: Entender estrutura PE/ELF, seções, imports
2. **Validação de resultados**: Interpretar o que a CNN "viu" no binário
3. **Feature engineering**: Criar features relevantes para baseline
4. **Análise de erros**: Entender por que certos malwares foram mal classificados

## Recursos

- [Intel Software Developer Manuals](https://www.intel.com/content/www/us/en/developer/articles/technical/intel-sdm.html)
- [AMD64 Architecture Programmer's Manual](https://www.amd.com/en/support/tech-docs)
- [PE Format Specification](https://docs.microsoft.com/en-us/windows/win32/debug/pe-format)
- [ELF Specification](https://refspecs.linuxfoundation.org/elf/elf.pdf)
