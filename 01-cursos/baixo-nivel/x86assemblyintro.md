# x86 Assembly Crash Course

> Resumo expandido da room **x86 Assembly Crash Course**, com foco em leitura de código durante análise de malware.

---

# 1. Por que Assembly importa?

Quando recebemos:

```text
malware.exe
```

não existe magicamente:

```text
malware.c
```

dentro dele.

O código-fonte foi compilado.

Por isso ferramentas como Ghidra tentam recuperar duas representações:

```text
Machine Code
     ↓
 Assembly
     ↓
Pseudo-C
```

O pseudo-C é ótimo.

Mas é uma **interpretação** do decompiler.

Assembly continua sendo a representação mais próxima do que realmente será executado pela CPU.

Então quando o pseudo-C ficar estranho:

> olhar o Assembly geralmente resolve a dúvida.

---

# 2. Não precisamos aprender a programar aplicações inteiras em Assembly

Nosso objetivo é diferente.

Não quero conseguir escrever:

```text
calculadora.asm
```

do zero.

Quero conseguir olhar:

```asm
xor eax, eax
push eax
call alguma_funcao
test eax, eax
jne 0x401245
```

e pensar:

> "Ele zerou EAX, chamou uma função, verificou o retorno e tomou uma decisão dependendo do resultado."

Isso já é extremamente útil.

---

# 3. Anatomia de uma instrução

Uma instrução Assembly geralmente possui:

```text
OPCODE OPERANDOS
```

Por exemplo:

```asm
mov eax, 5
```

Temos:

```text
mov → operação

eax → operando

5 → operando
```

---

# 4. Opcode

O **opcode** define qual operação a CPU deve executar.

Por exemplo:

```text
MOV
ADD
SUB
XOR
CALL
JMP
```

Internamente, a CPU não lê a palavra:

```text
MOV
```

Ela lê bytes.

Por exemplo, determinada instrução pode aparecer no binário como algo parecido com:

```text
B8 5F 00 00 00
```

O disassembler olha esses bytes e mostra:

```asm
mov eax, 0x5f
```

Então:

```text
Machine code → bytes

Assembly → representação humana desses bytes
```

---

# 5. Operand

O operando diz **com o que a operação será realizada**.

Os três tipos que mais aparecem são:

```text
Immediate
Register
Memory
```

---

# 6. Immediate operand

É um valor diretamente escrito na instrução.

```asm
mov eax, 5
```

O:

```text
5
```

é um immediate.

Outro exemplo:

```asm
cmp eax, 0
```

O `0` é immediate.

---

# 7. Register operand

Usa um registrador.

```asm
mov eax, ebx
```

Aqui:

```text
EAX → destination
EBX → source
```

Depois:

```text
EAX recebe o valor de EBX
```

EBX continua existindo normalmente.

---

# 8. Memory operand

Normalmente representado usando:

```text
[ ]
```

Exemplo:

```asm
mov eax, [ebx]
```

Isso NÃO significa:

```text
EAX = EBX
```

Significa:

```text
EBX contém um endereço

vá nesse endereço

pegue o valor que existe lá

coloque esse valor em EAX
```

Visualmente:

```text
EBX = 0x500000
         │
         ▼
Memória 0x500000
         │
         └── 0x12345678

mov eax,[ebx]

EAX = 0x12345678
```

Essa diferença é fundamental.

---

# 9. Endereço vs valor

Uma das coisas que mais confundem quando começamos:

```asm
mov eax, ebx
```

significa:

```text
copiar o valor de EBX
```

Enquanto:

```asm
mov eax, [ebx]
```

significa:

```text
usar EBX como endereço
e pegar o conteúdo daquele endereço
```

Compare:

```text
EBX = 0x500000

memória[0x500000] = 1337
```

Então:

```asm
mov eax, ebx
```

resulta em:

```text
EAX = 0x500000
```

Mas:

```asm
mov eax, [ebx]
```

resulta em:

```text
EAX = 1337
```

---

# 10. Little Endian

x86 usa **little endian**.

Isso significa que valores de múltiplos bytes são armazenados começando pelo byte menos significativo.

Por exemplo:

```text
0x12345678
```

pode aparecer na memória como:

```text
78 56 34 12
```

No começo isso parece coisa feita para infernizar estudante.

Depois você simplesmente acostuma.

Isso importa muito quando analisamos:

* dumps de memória;
* strings;
* endereços;
* shellcode;
* estruturas binárias;
* PE headers.

---

# 11. MOV

A instrução mais comum do universo:

```asm
mov destino, origem
```

Exemplo:

```asm
mov eax, 10
```

Agora:

```text
EAX = 10
```

Outro:

```asm
mov eax, ebx
```

Agora:

```text
EAX = valor de EBX
```

---

# 12. MOV não necessariamente significa "movimentar"

Apesar do nome **move**, pense:

> copiar.

Porque:

```asm
mov eax, ebx
```

não destrói EBX.

É aproximadamente:

```c
eax = ebx;
```

---

# 13. MOV usando memória

```asm
mov eax, [ebx]
```

Aproximadamente:

```c
eax = *ebx;
```

Enquanto:

```asm
mov [ebx], eax
```

é aproximadamente:

```c
*ebx = eax;
```

Isso ajuda bastante se você já entende ponteiros em C.

---

# 14. LEA — Load Effective Address

Essa instrução confunde todo mundo inicialmente.

```asm
lea eax, [ebx+4]
```

Ela **não acessa a memória em `EBX+4`**.

Ela calcula:

```text
EBX + 4
```

e coloca esse endereço em EAX.

Então:

```asm
mov eax, [ebx+4]
```

é:

> Pegue o conteúdo existente no endereço EBX+4.

Enquanto:

```asm
lea eax, [ebx+4]
```

é:

> Calcule o endereço EBX+4.

---

# 15. Exemplo LEA

Suponha:

```text
EBX = 1000
memória[1004] = 999
```

Então:

```asm
mov eax,[ebx+4]
```

gera:

```text
EAX = 999
```

Mas:

```asm
lea eax,[ebx+4]
```

gera:

```text
EAX = 1004
```

---

# 16. Por que LEA aparece tanto?

Porque além de endereços, compiladores conseguem usar LEA para fazer cálculos eficientes.

Por exemplo:

```asm
lea eax, [eax+eax*4]
```

é aproximadamente:

```text
eax = eax * 5
```

Então nem todo `LEA` significa que o programa está manipulando ponteiros.

---

# 17. NOP

```asm
nop
```

Significa:

```text
No Operation
```

A CPU basicamente:

> "ok 👍"

e segue para a próxima instrução.

NOP pode aparecer por:

* alinhamento;
* patching;
* compilação;
* exploits;
* shellcode.

Também existem os famosos:

```text
NOP sleds
```

de exploração clássica.

---

# 18. SHL e SHR

Shift desloca bits.

```asm
shl eax, 1
```

desloca bits para a esquerda.

Em muitos casos equivale aproximadamente a:

```text
eax × 2
```

Enquanto:

```asm
shr eax, 1
```

pode equivaler aproximadamente a:

```text
eax / 2
```

para valores apropriados.

---

# 19. ROL e ROR

Rotação é semelhante ao shift, mas os bits que "saem" de um lado entram pelo outro.

```text
ROL → rotate left
ROR → rotate right
```

Isso é particularmente interessante em malware.

Por quê?

Porque operações como:

```text
XOR
ROL
ROR
ADD
```

são muito usadas em:

* algoritmos de hashing;
* resolução dinâmica de APIs;
* criptografia simples;
* obfuscação.

Se você encontrar um loop cheio de:

```asm
ror eax, 13
add eax, edx
```

vale começar a suspeitar de algum algoritmo de hash.

---

# 20. Flags

Operações Assembly alteram bits do:

```text
EFLAGS
```

ou:

```text
RFLAGS
```

Alguns dos principais:

| Flag | Significado     |
| ---- | --------------- |
| `ZF` | Zero Flag       |
| `CF` | Carry Flag      |
| `SF` | Sign Flag       |
| `OF` | Overflow Flag   |
| `PF` | Parity Flag     |
| `AF` | Auxiliary Carry |
| `DF` | Direction Flag  |
| `IF` | Interrupt Flag  |

Para começar, foque principalmente:

```text
ZF
CF
SF
OF
```

---

# 21. ADD

```asm
add eax, 5
```

equivale aproximadamente:

```c
eax = eax + 5;
```

---

# 22. SUB

```asm
sub eax, 5
```

aproximadamente:

```c
eax = eax - 5;
```

Essas operações também alteram flags.

---

# 23. INC e DEC

```asm
inc eax
```

aproximadamente:

```c
eax++;
```

E:

```asm
dec eax
```

aproximadamente:

```c
eax--;
```

Aparecem bastante em loops.

---

# 24. MUL / IMUL

Multiplicação.

A diferença geral:

```text
MUL  → unsigned
IMUL → signed
```

Não vale a pena decorar todos os detalhes dos registradores envolvidos agora.

Só saiba reconhecer que existe multiplicação acontecendo.

---

# 25. DIV / IDIV

Divisão.

```text
DIV  → unsigned
IDIV → signed
```

Novamente, inicialmente o importante é reconhecer a intenção.

---

# 26. AND

Operação bitwise:

```asm
and eax, ebx
```

Pode ser usada para:

* aplicar máscaras;
* verificar bits;
* limpar bits.

Exemplo:

```asm
and eax, 0xFF
```

mantém apenas os últimos 8 bits.

---

# 27. OR

```asm
or eax, ebx
```

Pode ativar determinados bits.

Muito usado na manipulação de flags e bitmasks.

---

# 28. XOR

Essa instrução é MUITO importante em malware.

```asm
xor eax, ebx
```

realiza XOR bit a bit.

Uma propriedade extremamente útil:

```text
X XOR X = 0
```

Portanto:

```asm
xor eax, eax
```

resulta em:

```text
EAX = 0
```

Essa é uma maneira extremamente comum de zerar um registrador.

---

# 29. NÃO confunda todo XOR com criptografia

Quando começamos malware analysis é fácil fazer:

```asm
xor eax,eax
```

e pensar:

> MEU DEUS CRIPTOGRAFIA.

Não.

Isso normalmente é apenas:

```text
EAX = 0
```

Agora, se encontrarmos um loop parecido com:

```asm
mov al,[esi]
xor al,0x37
mov [esi],al
inc esi
loop ...
```

aí sim provavelmente existe alguma transformação/decodificação de dados.

---

# 30. XOR e strings em malware

Malware frequentemente tenta esconder strings como:

```text
powershell.exe
cmd.exe
https://servidor-c2...
CreateProcessW
```

Uma estratégia simples seria:

```text
string original
      ↓
XOR com chave
      ↓
bytes aparentemente aleatórios
```

Quando executa:

```text
bytes
 ↓
XOR novamente
 ↓
string original
```

Então em análise dinâmica podemos às vezes encontrar strings **depois que elas são descriptografadas em memória**.

Isso se conecta diretamente com a diferença entre análise estática e dinâmica.

---

# 31. NOT

Inverte os bits:

```text
0 → 1
1 → 0
```

Exemplo:

```asm
not eax
```

Não é tão frequente quanto XOR, mas aparece.

---

# 32. CMP

CMP é uma das instruções mais importantes para leitura de fluxo.

```asm
cmp eax, ebx
```

Conceitualmente ela faz:

```text
eax - ebx
```

Mas NÃO salva o resultado.

Ela apenas altera as flags.

Então:

```asm
cmp eax, ebx
je iguais
```

é aproximadamente:

```c
if (eax == ebx) {
    goto iguais;
}
```

---

# 33. Exemplo simples de IF

C:

```c
if (senha == 10) {
    acesso();
}
```

Assembly simplificado:

```asm
cmp eax, 10
jne acesso_negado

call acesso
```

A lógica:

```text
compare EAX com 10

se não for igual
    pule

caso contrário
    chame acesso()
```

---

# 34. TEST

TEST é parecido conceitualmente com AND:

```asm
test eax, eax
```

faz uma operação lógica e altera as flags, mas descarta o resultado.

O padrão:

```asm
test eax, eax
```

é MUITO comum.

Ele normalmente significa:

> EAX é zero?

Porque:

```text
0 AND 0 = 0
```

e então:

```text
ZF = 1
```

---

# 35. Padrão extremamente comum

```asm
call alguma_funcao
test eax, eax
jz erro
```

Mentalmente:

```text
resultado = alguma_funcao();

if (resultado == 0) {
    goto erro;
}
```

Quando começar a ler malware no Ghidra você verá isso o tempo inteiro.

---

# 36. CMP vs TEST

Simplificando:

```asm
cmp eax, ebx
```

serve muito bem para perguntar:

> EAX é igual/maior/menor que EBX?

Enquanto:

```asm
test eax, eax
```

é extremamente comum para perguntar:

> EAX é zero?

---

# 37. JMP

```asm
jmp endereco
```

É um salto incondicional.

Não pergunta nada.

É aproximadamente:

```c
goto endereco;
```

---

# 38. Conditional jumps

Esses saltos dependem das flags.

Os mais comuns:

| Instrução | Ideia             |
| --------- | ----------------- |
| `JE`      | jump if equal     |
| `JZ`      | jump if zero      |
| `JNE`     | jump if not equal |
| `JNZ`     | jump if not zero  |
| `JG`      | jump if greater   |
| `JL`      | jump if less      |
| `JGE`     | greater or equal  |
| `JLE`     | less or equal     |
| `JA`      | above             |
| `JB`      | below             |
| `JAE`     | above or equal    |
| `JBE`     | below or equal    |

---

# 39. JE e JZ

Na prática:

```text
JE
JZ
```

dependem do Zero Flag.

Depois de:

```asm
cmp eax, ebx
```

se forem iguais:

```text
resultado da subtração = 0
ZF = 1
```

Então:

```asm
je destino
```

é tomado.

---

# 40. Signed vs unsigned

Aqui temos uma armadilha.

```text
JG / JL
```

são normalmente usados para comparações **signed**.

Enquanto:

```text
JA / JB
```

são normalmente usados para comparações **unsigned**.

Então:

```text
G = Greater

A = Above
```

parecem significar a mesma coisa em inglês, mas trabalham com interpretações diferentes dos números.

Não precisa decorar toda a matemática agora.

Só guarde:

```text
JG/JL → signed

JA/JB → unsigned
```

---

# 41. Como IF vira Assembly

Código:

```c
if (x == 10) {
    malware();
} else {
    sair();
}
```

Pode virar algo parecido com:

```asm
cmp eax, 10
jne nao_igual

call malware
jmp fim

nao_igual:
call sair

fim:
```

Quando vemos vários:

```text
CMP
TEST
JMP
JE
JNE
```

estamos reconstruindo a lógica do programa.

---

# 42. Como LOOP vira Assembly

C:

```c
for (int i = 0; i < 10; i++) {
    fazer_algo();
}
```

Assembly simplificado:

```asm
mov ecx, 0

loop_inicio:
cmp ecx, 10
jge loop_fim

call fazer_algo
inc ecx

jmp loop_inicio

loop_fim:
```

Em malware, loops podem ser usados para:

* descriptografar buffers;
* procurar processos;
* enumerar arquivos;
* calcular hashes;
* procurar APIs;
* percorrer estruturas;
* verificar ambientes de análise.

---

# 43. Stack

A stack funciona em:

```text
LIFO
```

**Last In, First Out.**

Operações principais:

```text
PUSH
POP
CALL
RET
```

---

# 44. PUSH

```asm
push eax
```

coloca EAX no topo da stack.

Conceitualmente:

```text
antes

│ X │ ← ESP


push eax


depois

│ valor de EAX │ ← ESP
│ X            │
```

Em x86 tradicional a stack cresce em direção a endereços menores.

Então PUSH ajusta ESP/RSP de acordo.

---

# 45. POP

```asm
pop eax
```

remove o elemento do topo da stack e coloca em EAX.

```text
│ 1337 │ ← ESP

pop eax

EAX = 1337
```

---

# 46. PUSHA / PUSHAD

Existem instruções históricas que salvam vários registradores de uma vez.

```text
PUSHA
PUSHAD
```

Isso é particularmente interessante durante reversing.

Código manual, shellcode e alguns unpacking stubs podem querer:

```text
guardar estado dos registradores
      ↓
fazer um monte de coisa
      ↓
restaurar estado
```

Por isso sequências desse tipo podem chamar atenção.

Importante:

> Não assuma automaticamente "PUSHAD = malware packed".

É apenas um indício contextual.

---

# 47. CALL

```asm
call funcao
```

faz duas coisas conceitualmente:

```text
1. guarda onde precisa voltar

2. altera o fluxo para a função
```

Exemplo:

```asm
0x401000 call funcao
0x401005 mov eax, 5
```

O endereço:

```text
0x401005
```

precisa ser preservado.

Depois a função executa:

```asm
ret
```

e volta para lá.

---

# 48. CALL é extremamente importante em malware analysis

Principalmente quando conseguimos identificar uma API:

```asm
call CreateFileW
```

Já temos uma pista:

> O programa está mexendo com arquivos.

Outros exemplos:

```text
CreateProcessW
→ criação de processo

VirtualAlloc
→ alocação de memória

VirtualProtect
→ mudança de proteção de memória

RegSetValueEx
→ alteração de Registry

WinHttpOpen
→ comunicação HTTP

LoadLibrary
→ carregar DLL

GetProcAddress
→ localizar função dinamicamente
```

Uma grande parte de análise estática consiste em entender:

```text
qual função foi chamada
+
com quais argumentos
```

---

# 49. RET

```asm
ret
```

retorna para quem chamou a função.

Conceitualmente:

```text
CALL
 ↓
 função
 ↓
 RET
 ↓
 caller
```

---

# 50. Function Prologue

Podemos encontrar:

```asm
push ebp
mov ebp, esp
sub esp, 20h
```

Mentalmente:

```text
criar stack frame
+
reservar espaço para variáveis locais
```

---

# 51. Function Epilogue

Depois:

```asm
mov esp, ebp
pop ebp
ret
```

ou:

```asm
leave
ret
```

Mentalmente:

```text
desmontar frame
+
voltar
```

---

# 52. Um exemplo inteiro

Imagine:

```asm
push ebp
mov ebp, esp

mov eax, [ebp+8]
cmp eax, 5
jne erro

mov eax, 1
jmp fim

erro:
xor eax, eax

fim:
mov esp, ebp
pop ebp
ret
```

Vamos traduzir.

---

# 53. Linha por linha

```asm
push ebp
mov ebp, esp
```

Cria stack frame.

---

```asm
mov eax, [ebp+8]
```

Pega algum argumento.

Vamos chamar ele de:

```text
x
```

---

```asm
cmp eax, 5
jne erro
```

Pergunta:

```text
x == 5?
```

Se não:

```text
goto erro
```

---

```asm
mov eax, 1
jmp fim
```

Se era igual:

```text
return 1
```

---

```asm
erro:
xor eax, eax
```

Zera EAX.

Portanto:

```text
return 0
```

---

# 54. Pseudo-C

A função provavelmente seria algo semelhante a:

```c
int funcao(int x) {
    if (x == 5) {
        return 1;
    }

    return 0;
}
```

Isso é exatamente a habilidade que queremos desenvolver.

Não:

> decorar cada opcode.

Mas:

> transformar Assembly em comportamento compreensível.

---

# 55. Exemplo ligado a malware

Imagine:

```asm
call IsDebuggerPresent
test eax, eax
jne sair
```

Traduzindo:

```c
if (IsDebuggerPresent()) {
    sair();
}
```

Isso é uma técnica básica de:

```text
Anti-Debugging
```

E veja como só precisamos saber:

```text
CALL
TEST
JNE
EAX como retorno
```

para entender a lógica.

---

# 56. Outro padrão interessante

```asm
xor ecx, ecx

loop_decode:
mov al, [esi+ecx]
xor al, 37h
mov [esi+ecx], al
inc ecx

cmp ecx, 20h
jl loop_decode
```

Mesmo sem traduzir tudo perfeitamente:

```text
ECX começa em 0
      ↓
pega byte
      ↓
XOR com 0x37
      ↓
salva byte novamente
      ↓
incrementa contador
      ↓
repete
```

Hipótese:

> Existe um buffer de aproximadamente 0x20 bytes sendo transformado byte por byte usando XOR.

Isso pode ser:

* string escondida;
* configuração;
* URL;
* chave;
* payload pequeno.

---

# 57. Outro padrão comum em malware

```asm
call VirtualAlloc
mov ebx, eax
```

Se `VirtualAlloc` retorna o endereço da memória em EAX:

```text
EAX → memória recém-alocada
```

Então:

```asm
mov ebx,eax
```

preserva esse endereço em EBX.

Depois podemos encontrar:

```asm
mov [ebx], ...
```

ou algum loop copiando/descriptografando dados.

Finalmente:

```asm
call ebx
```

ou:

```asm
jmp ebx
```

Isso seria extremamente suspeito.

Raciocínio:

```text
alocou memória
      ↓
colocou conteúdo nela
      ↓
executou aquele endereço
```

Essa é exatamente a mentalidade útil para investigar loaders, packers e malware fileless.

---

# 58. Ghidra: como eu deveria ler Assembly?

Não tente ler assim:

```text
Linha 1
Linha 2
Linha 3
Linha 4
Linha 5
Linha 6
...
```

Tente procurar **blocos lógicos**.

Exemplo:

```asm
call CreateFileW
cmp rax, -1
je falhou
```

Mentalmente transforme imediatamente em:

```text
tenta abrir arquivo

se falhar
    vai para falhou
```

Você não precisa lembrar cada detalhe.

---

# 59. Padrões que quero reconhecer instantaneamente

## Zerar registrador

```asm
xor eax,eax
```

=

```text
EAX = 0
```

---

## Comparar com zero

```asm
test eax,eax
```

=

```text
EAX == 0?
```

---

## Comparar valores

```asm
cmp eax,5
```

=

```text
EAX comparado com 5
```

---

## Condição

```asm
je destino
```

=

```text
se igual → destino
```

---

## Chamar função

```asm
call destino
```

=

```text
executar função
```

---

## Acessar memória

```asm
mov eax,[ebx]
```

=

```text
EAX = memória apontada por EBX
```

---

## Obter endereço

```asm
lea eax,[ebx+4]
```

=

```text
EAX = endereço EBX+4
```

---

# 60. Por que isso se conecta diretamente com análise estática?

Quando eu chegar em **Advanced Static Analysis**, o Ghidra vai me mostrar coisas como:

```asm
MOV
LEA
CALL
CMP
TEST
JNZ
XOR
```

A room de Assembly não serve para me transformar em programador Assembly.

Serve para que esses nomes parem de parecer magia negra.

---

# 61. Por que isso se conecta com análise dinâmica?

No x64dbg eu poderei literalmente acompanhar:

```text
RAX
RBX
RCX
RDX
RSP
RBP
RIP
```

e executar:

```text
uma instrução
      ↓
ver registradores mudarem
      ↓
outra instrução
      ↓
ver flags mudarem
      ↓
CALL
      ↓
entrar na função
```

Esse é o ponto em que Assembly começa a fazer muito mais sentido.

Ler Assembly sem executar é abstrato.

Dar **Step Into** e assistir EAX mudar de `0` para `1` torna tudo bem mais concreto.

---

# 62. Relação com strings

Um dos pontos mais interessantes para análise de malware.

Na análise estática podemos executar algo como:

```text
strings malware.exe
```

e encontrar:

```text
Microsoft
kernel32.dll
...
```

Mas uma string importante pode estar criptografada.

Assembly pode revelar:

```text
loop
 ↓
XOR
 ↓
grava memória
```

Então durante a execução a string passa a existir em plaintext.

Isso explica por que ferramentas como FLOSS são interessantes:

```text
strings normais
+
tentativa de recuperar strings construídas/decodificadas
```

---

# 63. Relação com packing

Um malware packed pode inicialmente conter:

```text
Unpacking Stub
```

em vez do programa real.

Esse stub pode:

```text
alocar memória

descompactar/descriptografar conteúdo

alterar proteção de memória

transferir execução
```

No Assembly podemos procurar justamente essa mudança:

```text
loader
 ↓
unpacking
 ↓
JMP/CALL
 ↓
Original Entry Point
```

Por isso Assembly é especialmente importante quando análise estática básica começa a falhar.

---

# 64. Relação com pesquisa em malware

Para pesquisa experimental envolvendo análise estática/dinâmica, esse conteúdo ajuda a entender **por que determinadas ferramentas conseguem ou não recuperar informação**.

Por exemplo:

```text
strings diretamente no executável
```

só encontram aquilo que está presente de maneira relativamente clara no arquivo.

Mas se o programa faz:

```text
XOR
loops
cópia para memória
unpacking
construção dinâmica
```

determinadas informações só aparecem:

* após algum tipo de análise avançada;
* depois do unpacking;
* ou durante execução.

Isso é uma conexão importante entre:

```text
Assembly
↓
obfuscação
↓
strings
↓
packing
↓
diferença entre análise estática e dinâmica
```

---

# 65. Cheat Sheet

## Movimento

```asm
mov dst, src
```

Copia valor.

```asm
lea dst, [addr]
```

Calcula endereço.

```asm
nop
```

Não faz nada.

---

## Matemática

```asm
add
sub
inc
dec
mul
imul
div
idiv
```

---

## Lógica

```asm
and
or
xor
not
```

---

## Comparações

```asm
cmp
test
```

---

## Fluxo

```asm
jmp

je / jz
jne / jnz

jg
jl
jge
jle

ja
jb
jae
jbe
```

---

## Stack

```asm
push
pop
```

---

## Funções

```asm
call
ret
```

---

# 66. Os 10 padrões que eu quero reconhecer sem pensar

```asm
xor eax,eax
```

→ `EAX = 0`

```asm
test eax,eax
```

→ verificar se EAX é zero

```asm
cmp eax,5
```

→ comparar EAX com 5

```asm
je X
```

→ pular se igual

```asm
jne X
```

→ pular se diferente

```asm
call X
```

→ chamar função

```asm
ret
```

→ retornar

```asm
mov eax,[ebx]
```

→ ler memória

```asm
mov [ebx],eax
```

→ escrever memória

```asm
lea eax,[ebx+4]
```

→ calcular endereço

Se isso estiver confortável, já existe uma base suficiente para começar reversing básico.

---

# 67. Como estudar essa room sem perder tempo

Minha ordem seria:

```text
1. entender registradores

2. MOV e memória

3. LEA

4. XOR

5. CMP

6. TEST

7. JE/JNE/JMP

8. PUSH/POP

9. CALL/RET

10. abrir debugger e ver isso acontecendo
```

Não gastaria horas decorando:

```text
PF
AF
DF
IF
```

agora.

Eles podem ser aprendidos quando aparecerem em um contexto real.

---

# 68. Meta de aprendizado

Depois dessa room eu deveria conseguir olhar:

```asm
call sub_401000
test eax,eax
jz loc_402000

mov rcx,rax
call sub_403000

jmp loc_404000
```

e mesmo sem saber o que `sub_401000` faz, pensar:

```text
chama função
 ↓
verifica retorno
 ↓
se zero → caminho A
 ↓
se não zero → usa retorno como argumento
 ↓
chama outra função
 ↓
continua
```

Se eu consigo fazer isso, a room cumpriu o papel dela.

Não preciso saber Assembly inteiro.

Preciso conseguir **seguir o raciocínio do programa**.
