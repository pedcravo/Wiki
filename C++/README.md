# C++
Nesta sessão vamos estudar sobre C++, seus conceitos, equações e prática.

Toda a parte prática vamos usar o diretório [Aprendendo C++][pratica].

## Tópicos:
- [C++](#c)
  - [Tópicos:](#tópicos)
  - [Conceitos](#conceitos)
    - [Fluxos de entrada e saída:](#fluxos-de-entrada-e-saída)
    - [Variáveis, Constantes e Ponteiros:](#variáveis-constantes-e-ponteiros)
      - [Variáveis](#variáveis)
      - [Ponteiros](#ponteiros)
      - [Constantes](#constantes)
    - [Funções](#funções)
      - [main()](#main)
  - [Tipos de Erros](#tipos-de-erros)
    - [Erro de sintaxe:](#erro-de-sintaxe)
    - [Erro de semântica:](#erro-de-semântica)
    - [Erro de compilação:](#erro-de-compilação)
    - [Erro de vinculação (link):](#erro-de-vinculação-link)
    - [Erro de execução:](#erro-de-execução)
    - [Erro de lógica:](#erro-de-lógica)
  - [Criar arquivo executável](#criar-arquivo-executável)
  - [Links](#links)

## Conceitos

- `return` → É usado para retornar um valor (variável, constante e etc.) ao sistema ou a máquina, como: `return 0;`, `return a;`.

- `namespaces` → Usados para renomear comandos, como: `std::cout` que pode virar `cout`.

- `cin` → Entrada padrão para o teclado, recebe dados do teclado.
- `cout` → Saída padrão de dados no prompt, mostra no prompt algum dado.
- `cerr` → Saída de erros padrão, mostra erros.
- `clog` → Saída dos logs padrão, mostra logs.
- `<<` → Usa dados anteriores como argumentos para o comando/variável anterior (geralmente anda junto com `cout`).
- `>>` → Usa dados anteriores para o comando/variável a seguir.
- `endl` → Pula linha no prompt (endl - end line).

### Fluxos de entrada e saída:
- Saída de dados (da máquina para o usúario)
  ```cpp
  cout << data1;

  cout << "data 1 is" << data1;

  cout << "data 1 is" << data1 << endl;
  cout << "data 1 is" << data1 << "\n";
  ```
- Entrada de dados (do teclado para a máquina)
  ```cpp
  cin >> data1;

  cout >> data1 >> data2;
  ```
  > A entrada de dadps pode falhar dependendo da entrada e do tipo de dado solicitado (*int* recebe *string*)

### Variáveis, Constantes e Ponteiros:
Ambos tem conceitos semelhantes por se tratarem de nomear, apontar e definir locais da memória.

Pense na memória como uma caixa de correio de um prédio, onde cada caixinha tem um espaço para conteúdo e um endereço de identificação.

<img src="https://https://github.com/pedcravo/Wiki/blob/main/C%2B%2B/memoria.jpg" width="600px">

É possível dar um nome para cada caixinha com base nos moradores de cada apartamento e ao invés de chamar a caixinha pelo endereço chamá-la pelo nome. Cada caixinha pode ter armazenados qualquer tipo de coisa, desde cartas até chaves.

Logo podemos inferir que **variáveis** e **ponteiros** são nomes dados a locais especificos na memória, tendo cada um tem seu prórpio endereço e conteúdo volátil. A única diferença entre elas são os tipos de contéudo que armazenam (veremos isso em breve).

Já as **constantes** podem ser vistas como caixinhas semelhantes as variáveis e ponteiros mas que não podem ter seu tipo ou conteúdo modificados com o decorrer do tempo.

#### Variáveis
Como vimos são palavras chaves para locais na memória que armazenam valores em sí mesmos.

Como se fosse uma caixinha de correspondencia que tem o nome de José (morador daquele apto) que contém somente panfletos, voltando ao exemplo da caixa de correio.

Cada variável tem seu **tipo**, seu **nome**, seu **valor** e seu **escopo**. Sendo a sintaxe comum:

```html
<tipo> <nome> = <valor>;
```

**Tipos de variáveis:**
- `int` → Números inteiros (10,-20,0);
- `long` → Números inteiros grandes (2000000);  
- `float` → Números flutuantes (1.01);
- `double` → Números flutuantes grandes (1.00001);
- `bool` → Boleanos (true/false, 0/qualquer-valor); 
- `char` → Representam caracteres (A, X, @), tipos (`char`, `char16_t`, `char32_t`, `wchar_t`)
- `string` → Conjunto de caracteres (batata);

**Modificadores de variáveis:**
- `signed` → Adicina sinal ao tipo de variável;
- `unsigned` → Retira sinal ao tipo de variável;
- `short` → Torna o tamanho da variável menor;
- `long` → Aumentar o tamanho da variável.

<img src="https://https://github.com/pedcravo/Wiki/blob/main/C%2B%2B/MidifierslnC.png" width="600px">

**Nomes de variáveis:**
- Existem casos convencionais para as declarações dos nomes de váriaveis.

[Casos comuns para declaração de variáveis →][variavel]

**Escopo:**
É em outras palavras é a área em que a variável existe e quem pode acessa-la, fora da área essa variável não existe mas todos que estiverem dentro da área pode acessa-la.

Ou seja, variáveis criadas em funções só existem dentro daquelas funções e enquanto as funções existirem, só podem ser acessadas por funções, operações e ações dentro delas.

| Escopo | Descrição                                                                                                                                            |
| :----: | :--------------------------------------------------------------------------------------------------------------------------------------------------- |
| Local  | Variáveis inicializadas dentro de funções, que podem ser acessadas por todos em seu contexto e que deixam de existir fora de suas funções.           |
| Global | Variáveis que são inicializadas fora das funções (na área geral do programa), podem ser acessadas por todos e existem até que o programa se encerre. |

**Exemplos:**

```cpp
int a = 10;
```
- Inicializando variável estilo C.

```cpp
float b, c;
b = 3,14;
c = 111,11;
```
- Declarando variáveis e em seguida atribuindo valores a elas.

```cpp
int d (21);
```
- Inicializando variável estilo construtor.

```cpp
int e {8};
char f {'J'};
```
- Inicializando variável estilo C++11.

#### Ponteiros
Como dito anteriormente, são nomes dados a locais da memória que armazenam conteúdos específicos. Os conteúdos armazenados por esses ponteiros são os endereços de outros locais na mémoria.

Voltando ao exemplo das caixas de correios, ponteiros seriam uma caixinha com o nome de João que tem uma chave para caixinha de correspondencia de José. O conteúdo da caixinha de João é uma forma de encontrar e ver o que tem dentro da caixinha de José.

#### Constantes
Como já disse são variáveis ou ponteiros que tem seu tipo e valor definidos uma única vez no código, após sua definição não podem ter seu valor alterado.

**Contantes literais:**
```cpp
const int x = 12;
const float y = 1.56;
const string name = "Andrew";
```

**Constantes definidas:**
```cpp
#define pi 3.1415926;
```
> Usado principalmente em sistemas legados.

### Funções

#### main()
A função `main()` é a principal função de qualquer software, pois ela que roda ao inciar o programa.
Podemos ver a sintaxe padrão:

```cpp
int main()
{
  //codigo
  return 0;
}
```
```bash
$ programa.exe
```

A função `main()` pode precisar de argumentos para funcionar, neste caso seria assim o código:

```cpp
int main(int arg1, char *arg2[])
{
  //codigo
  return 0;
}
```
```bash
$ programa.exe arg1 arg2
```

## Tipos de Erros
### Erro de sintaxe:
Erro na estrutura do código.

Exemplo:
```cpp
std::cout << "Errors" >> std::endl
return
```

### Erro de semântica:
Erros no sentido do código.

Exemplo:
```cpp
int a = 0;
string b;
a + b;
```

### Erro de compilação:

### Erro de vinculação (link):
Erros ao fazer vinculação entre códigos, detectados na build.

Exemplo:
```cpp
extern x;

int main ()
{
  std::cout << x >>;
}
```

### Erro de execução:
Erros que fazem o programa crachar.

Exemplo:
- Divisão por 0;
- Arquivo não encontrado;
- Falta de memória.

### Erro de lógica:
Erros na lógica do programador, nenhum erro de escrita ou semantica, mas sim na lógica da escrita.
O programa executa mas não do jeito na qual o programador gostaria.

Exemplo:
```cpp
int a = 10;
for (a; a < 10; a++){...}
```

## Criar arquivo executável

`$ sudo apt install g++` →  Instala compilador C++

`$ sudo apt install gdb` → Instala debugger C++

Uma aplicação em C++ pode rodar em modo **Release** ou **Debug**.
O modo “**Debug**” é utilizado durante o desenvolvimento para facilitar a depuração, é focado nos testes e encontrar bugs, enquanto o modo “**Release**” é usado para criar uma versão final otimizada para implantação em um ambiente de produção, é focado em velocidade e execução.

**`$ g++ c.cpp`** → Cria arquivo executável padrão `a.out`.

**`$ g++-13 -g -ggdb -std=c++23 app.cpp -o APP`**  → Cria arquivo executável em modo debugger.

`g++-13` → Versão do compilador.

`-g -ggdb` → Torna o arquivo debugavel.

`-std=c++23` → Versão da linguagem.

`app.cpp` → Arquivo padrão.

`-o APP` → Renomeia o executável padrão para APP.

**`$ g++-13 -On -std=c++23 app2.cpp -o APP`** → Cria arquivo executável com flags de compilação.

`-On` → Flags de compilação, onde o `n` define a flag (`0` a `3`).

`-O0` →

`-O1` →

`-O2` →

`-O3` → Modo **Release**.

Método padrão: `g++-13 -g -ggdb -std=c++23 .cpp; mv ~/Ontick/`

**Executar arquivo C++**

`$ ./a.out` → Executa executável padrão de C++.

[Tutorial Compilador →][compilador]

## Links
[Diretório parte prática →][pratica]

[Tutorial Compilador →][compilador]

[Casos comuns para declaração de variáveis →][variavel]

[pratica]: https://github.com/pedcravo/Aprendendo-C-
[variavel]: https://www.dio.me/articles/breve-guia-para-estilo-de-nomenclatura-para-programacao
[compilador]: https://www.tutorialspoint.com/gnu_debugger/index.htm