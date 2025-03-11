# C++
Nesta sessão vamos estudar sobre C++, seus conceitos, equações e prática.

Toda a parte prática vamos usar o diretório [Aprendendo C++][pratica].

## Tópicos:
- [C++](#c)
  - [Tópicos:](#tópicos)
  - [Conceitos](#conceitos)
    - [Expressões](#expressões)
      - [Expressões de tipo misto](#expressões-de-tipo-misto)
        - [Alto vs Baixo](#alto-vs-baixo)
        - [Mudança de tipos](#mudança-de-tipos)
    - [Instruções](#instruções)
    - [Operadores](#operadores)
        - [Procedência dos operadores:](#procedência-dos-operadores)
      - [Associação](#associação)
      - [Aritmético](#aritmético)
      - [Incremento/Decremento](#incrementodecremento)
        - [Incremento de "a" por "b"](#incremento-de-a-por-b)
        - [Incremento por 1](#incremento-por-1)
      - [Comparação e igualdade](#comparação-e-igualdade)
      - [Relacional](#relacional)
      - [Lógico](#lógico)
        - [Avaliação curto-circuito](#avaliação-curto-circuito)
      - [Acessar membro](#acessar-membro)
      - [Outros](#outros)
    - [Variáveis, Constantes e Ponteiros](#variáveis-constantes-e-ponteiros)
      - [Variáveis](#variáveis)
      - [Ponteiros](#ponteiros)
      - [Constantes](#constantes)
    - [Arrays](#arrays)
      - [Arrays multidimensionais:](#arrays-multidimensionais)
      - [Array 2D](#array-2d)
    - [Vetores](#vetores)
    - [Fluxos de entrada e saída](#fluxos-de-entrada-e-saída)
    - [Estruturas](#estruturas)
      - [Estruturas de Sequência](#estruturas-de-sequência)
      - [Estruturas de Seleção - Condicionais](#estruturas-de-seleção---condicionais)
        - [IF](#if)
        - [IF-ELSE](#if-else)
        - [IF-ELSEIF-ELSE](#if-elseif-else)
        - [IF (encadeado)](#if-encadeado)
        - [SWITCH](#switch)
        - [? Condicional](#-condicional)
      - [Estruturas de Iteração - Looping](#estruturas-de-iteração---looping)
        - [FOR](#for)
        - [WHILE](#while)
        - [DO-WHILE](#do-while)
- [WIP](#wip)
    - [Include](#include)
      - [rapidjson](#rapidjson)
        - [Estrutura e Comandos](#estrutura-e-comandos)
        - [Verificar se um membro existe](#verificar-se-um-membro-existe)
        - [Acessar um valor do JSON](#acessar-um-valor-do-json)
        - [Verificar o tipo de um valor](#verificar-o-tipo-de-um-valor)
        - [Obter valores do JSON](#obter-valores-do-json)
        - [Acessar elementos de um array](#acessar-elementos-de-um-array)
        - [Adicionar membros a um objeto JSON](#adicionar-membros-a-um-objeto-json)
        - [Adicionar elementos a um array](#adicionar-elementos-a-um-array)
      - [jsoncpp](#jsoncpp)
      - [glaze](#glaze)
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
**C++** ou Cpp é uma linguagem de programação Imperativa e Orientada a Objetos, é derivada do C. Devido sua descendência foi chamada por muito tempo por "*C whit classes*".

### Expressões
Expressões são blocos de códigos que são usados para formar [Instruções](#instruções), como:
  - 34 (número);
  - fav_number (variável);
  - a + b (soma);
  - a * b (multiplicação);
  - a > b (relação);
  - a = b (atribuição);

#### Expressões de tipo misto
Assim como toda linguagem de programação, em C++ é possível fazer operações entre variáveis de tipos diferentes. Dependendo de quais os tipos de variáveis e quais suas posições na hierarquia, pode haver perda de precisão dos dados.

##### Alto vs Baixo
Os "tipos" (Alto e Baixo) de variáveis são baseadas no tamanho dos valores que podem elas armazenar em relação aos outros tipos de variáveis. A hierarquia é:
1. long double;
2. double;
3. float;
4. unsigned long;
5. long;
6. unsigned int;
7. int.

Enquanto isso `short` e `char` são sempre transformados em `int`.

##### Mudança de tipos
Chamamos de "*conversão de tipos*" a mudança de tipo de data de um operador.
| Conversão | Descrição                                                                                                                                        |
| :-------: | :----------------------------------------------------------------------------------------------------------------------------------------------- |
| Promoção  | **Conversão para um tipo mais alto.** Geralmente usado em expressões matemáticas de forma implícita (não declara que vai haver mudança de tipo). |
| Regressão | **Conversão para um tipo mais baixo.** Geralmente usado em associação a tipos inferiores de forma implícita.                                     |

**Exemplos:**

```cpp
2 * 5.2                         //low <ope> high
```
↳ **Promoção implícita**: 2 é promovido para 2.0 para que seja possível realizar a equação (não é declarado pelo dev que vai haver mudança de tipo).

```cpp
int a = 100, b = 8;
double var = 0.0;
var = a / b;                    // resulta em 12
var static_cast<double>(a)/b    // resulta em 12.5
```
↳ **Promoção explícita**: a variável "a" é transformada momentaneamente em `double` para que o resultado da operação seja um `double` e não um `int` armazenado em `double`.

```cpp
int num = 0;
num = 123.321                   //low = high
```
↳ **Regressão implícito**: 123.321 é reduzido para 123 para que seja possível alocar o dado na memória (não é declarado pelo dev que vai haver mudança de tipo).


### Instruções
Instruções são linhas de códigos que executam ações. Geralmente terminadas em ";".

| Códigos                                    | Tipos de instruções |
| :----------------------------------------- | :-----------------: |
| `int x;`                                   |     Declaração      |
| `fav_number = 12;`                         |     Atribuição      |
| `x = 2 * 5;`                               |     Atribuição      |
| `1.5 + 2.8;`                               |      Expressão      |
| `if (a > b) cout << "ais greater than b";` |         If          |


### Operadores
São grupos de caracteres usados para formar expressões. Os operadores podem ser divididos em 3 classes principais:

- **Unários** → São operadores que usam 1 operando, geralmente usados para negar o operando.
- **Binários** → A maioria dos operadores se encaixam nessa classe, pois usam 2 operandos para realizar suas operações.
- **Terciários** → Existem operadores que usam 3 operandos, porém é mais raro seu uso.

Os operadores também podem ser agrupados em cerca de 7 grupos:

##### Procedência dos operadores:
Do mais alto para o mais baixo.

| Operador                           | Associação    |
| :--------------------------------- | :------------ |
| [] -> . ()                         | left to right |
| ++ -- -(unario) *(de-ref) & sizeof | right to left |
| * / %                              | left to right |
| + -                                | left to right |
| << >>                              | left to right |
| < <= > >=                          | left to right |
| == !=                              | left to right |
| &                                  | left to right |
| ^                                  | left to right |
| \|                                 | left to right |
| &&                                 | left to right |
| \|\|                               | left to right |
| = op= ?:                           | right to left |

> A tabela não está completa

- Ao usar operadores diferentes, é usada a regra de **procedência**, qual tiver a procedência mais alta é executador primeiro.
- Quando ambos os operadores tem a mesma procedência ou são iguais, a regra da **associatividade** é utilizada, da esquerda para a direita ou da direita para esquerda.

#### Associação
Usados para atribuir o valor da direita a variável da esquerda. Fluxo de atribuição da direita para a esquerda em grupos de 2.

Após a atribuição de um valor a uma variável, a mesma é substituída pelo valor para ser associada a outra variável.

É impossível atribuir um tipo de valor a um tipo diferente de variável.

**Membros:**
- `=` → Igual

**Exemplos:**
```cpp
float var1;
var1 = 1.1;
```
↳ Faz a atribuição de variável.

```cpp
int var2, var3;
var2 = var3 = 2;
```
↳ Realiza a atribuição de variáveis em cadeia.

```cpp
int var4 = "value";
```
↳ Impossível de realizar a atribuição, pois são tipos diferentes.

#### Aritmético
Usados para manipular valores numéricos.

**Membros:**
- `+` → Adição
- `-` → Subtração
- `*` → Multiplicação
- `/` → Divisão
- `%` → Modulo ou resto da divisão

**Exemplos:**
```cpp
1 + 3;
```
↳ Faz soma entre valores.

```cpp
int var1, var2 = 4;
var1 = var2 * 2;
```
↳ Realiza a atribuição da variável var1 como sendo a multiplicação da var2 por 2.

#### Incremento/Decremento

##### Incremento de "a" por "b"
São operadores que funcionam em parte de forma semelhante ao Operador de Atribuição e parte como os Operadores Aritméticos.

Existem para incrementar a variável "a" por qualquer valor. São mais versáteis e ocupam menos espaço, geralmente utilizados em loops.

Forma geral: 
```html
a <operador> b
```

| Operador | Significado | Exemplo em código |
| :------: | :---------- | :---------------: |
|   `+=`   | a = a + b   |     `a += b;`     |
|   `-=`   | a = a - b   |     `a -= b;`     |
|   `*=`   | a = a * b   |     `a *= b;`     |
|   `/=`   | a = a/b     |     `a /= b;`     |
|   `%=`   | a = a%b     |     `a %= b;`     |
|  `>>=`   | a = a >> b  |    `a >>= b;`     |
|  `<<=`   | a = a << b  |    `a <<= b;`     |
|   `&=`   | a = a & b   |     `a &= b;`     |
|   `^=`   | a = a ^ b   |     `a ^= b;`     |
|  `\|=`   | a = a \| b  |    `a \|= b;`     |

**Exemplos:**
```cpp
int a = 10;
a += 20;
```
↳ Faz soma de a com 20 que resulta no valor de "a".

```cpp
a /= 2;
```
↳ Divide "a" por 2 e iguala a "a".

```cpp
int b = 5, c = 15;
a *= b + c; // a = a*(b + c)
```
↳ Resolve equação "a*(b + c)" comprimindo os operadores.


##### Incremento por 1
Semelhantes aos que incrementam "a" com "b", os operadores de incremento por 1, fazem operações somente com a variável e com 1. São mais simples e práticos.

Eles existem para fazer a adição ou subtração por 1 de forma mais reduzida no código. Geralmente usados em loops para percorrer uma `string`, `array` ou `vetor`.

**Membros:**
- `++` → Incremento por 1
- `--` → Decremento por 1

Eles podem ser usados antes ou depois da variável, tendo cada um seu sentido:
- Prefixo → `++num`
- Sufixo → `num++`

**Exemplos:**
```cpp
result = ++counter;
cout << "Counter: " << counter << endl;
cout << "Resulta: " << result << endl;
```
↳ Faz um pré-incremento, incrementa **primeiro o counter e depois atribui valor ao result**;

```cpp
result = counter++;
cout << "Counter: " << counter << endl;
cout << "Resulta: " << result << endl;
```
↳ Realiza um pos-incremento, **primeiro atribui valor de counter ao result e após isso incremento counter**.

```cpp
result = ++counter + 10;
cout << "Counter: " << counter << endl;
cout << "Resulta: " << result << endl;
```
↳ Realiza um pre-incremento, **primeiro o counter e depois atribui valor de counter + 10 ao result**.


#### Comparação e igualdade
São operadores utilizados para comparar duas expressões, variáveis, números e etc. A saída destes operadores sempre é um `boolean` (true ou false).

Geralmente são utilizados em *loop* e *condicionais* para direcionar o andamento dos comandos.

**Membros:**
- `==` → Igual (checa se a igualdade é verdadeira)
- `!=` → Diferente (checa se a não igualdade é verdadeira)

**Exemplos:**
```cpp
a == b;
```
↳ Realiza checagem se `a` é igual a `b`;

```cpp
int var1 = 0, var2 = 10;
while (var1 != var2){'
  var1++;
}
```
↳ Executa `while` enquanto `var1` for diferente de `var2`;

```cpp
bool equal = false;
equal = (100 == 50+50);
cout << equal << endl;          //  0 ou 1
cout << boolalpha;              // muda formato
cout << equal << endl;          // false ou true
cout << noboolalpha;            // volta para formato original
```
↳ Mostra `equal` na tela de formatos diferentes, usando *0* e *1* bem como *false* e *true*;

#### Relacional
Semelhantes aos Operadores de comparação de igualdade, os operadores relacionais fazem comparação entre dois números, expressões, variáveis, dentre outros, e retorna um valor `boolean`.

**Membros:**
- `>` → Maior que
- `>=` → Maior ou igual
- `<` → Menor que
- `<=` → Menor ou igual
- `<=>` → Comparação de 3 vias (C++20)

#### Lógico
Esses operadores utilizam a tabela verdade (`boolean`) para funcionar, são a versão prática da tabela verdade.

Geralmente são utilizados em *condicionais* e *loops* para direcionar o andamento dos comandos.

**Membros:**
- *not* `!` → Negação (operador unário)
- *and* `&&` → E lógico (operador binário)
- *or* `||` →  OU lógico (operador binário)

<img src="https://https://github.com/pedcravo/Wiki/blob/main/C%2B%2B/TabelaVerdade.png" width="600px">

**Precedência:**
- *not* é superior ao *and*.
- *and* é superior ao *ou*.

##### Avaliação curto-circuito
A avaliação curto-circuito é quando o programa não analisa sempre todas as expressões para definir o valor final.
É uma avaliação que é utilizada comumente pelas linguagens de programação.

**Exemplos:**

```cpp
expr1 && expr2 && expr3
```
↳ Caso o resultado da primeira seja ***false*** o programa não lê as demais expressões, pois neste caso sempre será ***false***.

```cpp
expr1 || expr2 || expr3
```
↳ Caso o resultado da primeira expressão seja ***true*** o programa não lê as demais expressões, pois neste caso sempre será ***true***.

#### Acessar membro

#### Outros


### Variáveis, Constantes e Ponteiros
Ambos tem conceitos semelhantes por se tratarem de nomear, apontar e definir locais da memória.

Pense na memória como uma caixa de correio de um prédio, onde cada caixinha tem um espaço para conteúdo e um endereço de identificação.

<img src="https://https://github.com/pedcravo/Wiki/blob/main/C%2B%2B/memoria.jpg" width="600px">

É possível dar um nome para cada caixinha com base nos moradores de cada apartamento e ao invés de chamar a caixinha pelo endereço chamá-la pelo nome. Cada caixinha pode ter armazenados qualquer tipo de coisa, desde cartas até chaves.

Logo podemos inferir que **variáveis** e **ponteiros** são nomes dados a locais específicos na memória, tendo cada um tem seu próprio endereço e conteúdo volátil. A única diferença entre elas são os tipos de conteúdo que armazenam (veremos isso em breve).

Já as **constantes** podem ser vistas como caixinhas semelhantes as variáveis e ponteiros mas que não podem ter seu tipo ou conteúdo modificados com o decorrer do tempo.

#### Variáveis
Como vimos são palavras chaves para locais na memória que armazenam valores em sí mesmos.

Como se fosse uma caixinha de correspondência que tem o nome de José (morador daquele apto) que contém somente panfletos, voltando ao exemplo da caixa de correio.

Cada variável tem seu **tipo**, seu **nome**, seu **valor** e seu **escopo**. Sendo a sintaxe comum:

```html
<tipo> <nome> = <valor>;
```

**Tipos de variáveis:**
- `int` → Números inteiros (10,-20,0);
- `long` → Números inteiros grandes (2000000);  
- `float` → Números flutuantes (1.01);
- `double` → Números flutuantes grandes (1.00001);
- `bool` → Boolean (true/false, 0/qualquer-valor); 
- `char` → Representam caracteres (A, X, @), tipos (`char`, `char16_t`, `char32_t`, `wchar_t`)
- `auto` → Deixa o compilador decidir qual tipo vai ser usado com base no contexto do programa;
- `string` → Conjunto de caracteres ("batata");
- `string view` → String nãr armazenada que pode ser acessada mas não modificada, lembra o funcionamento de ponteiros.

> Os tipos `string` e `string_view` devem ser importados para serem utilizados no programa.
> Ao usa-los é necessário uso de `std::` como prefixo.

**Modificadores de variáveis:**
- `signed` → Adiciona sinal ao tipo de variável;
- `unsigned` → Retira sinal ao tipo de variável;
- `short` → Torna o tamanho da variável menor;
- `long` → Aumentar o tamanho da variável.

<img src="https://https://github.com/pedcravo/Wiki/blob/main/C%2B%2B/MidifierslnC.png" width="600px">

**Nomes de variáveis:**
- Existem casos convencionais para as declarações dos nomes de variáveis.

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
↳ Inicializando variável estilo C.

```cpp
float b, c;
b = 3,14;
c = 111,11;
```
↳ Declarando variáveis e em seguida atribuindo valores a elas.

```cpp
int d (21);
```
↳ Inicializando variável estilo construtor.

```cpp
int e {8};
char f {'J'};
```
↳ Inicializando variável estilo C++11.

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
 
### Arrays
Arrays são matrizes que contém dados estruturados, ou seja, são tipos de dados que contém uma série de dados.

Como por exemplo a pontuação de um teste. Onde o professor pode criar uma variável para armazenar cada valor ou armazenar todos em apenas uma array.
```cpp
int teste_nota1 = 0;
int teste_nota2 = 0;
int teste_nota3 = 0;
int teste_nota4 = 0;
...
int teste_notaN = 0;
```

**Caracteristicas:**
- Cada array tem seu tamanho fixo;
- Array é guardada na memória continuamente;
- Todos os elementos devem ser do mesmo tipo (int, float, char);
- Os elementos podem ser acessados diretamente e individualmente;
- O primeiro elemento tem index 0 enquanto o ultimo tem n-1.

**Declarando array:**
```html
<tipo> <nome> [<tamanho>] {<valores>};
```

**Exemplos:**
```cpp
int notas [10];
```
↳ Apenas declara array e define seu tamanho.

```cpp
int pontuacao [5] {10,7,2,8,9};
```
↳ Inicializa array com seu tamanho e valores definidos.

```cpp
int dias [7] {3,4};
```
↳ Incializa array com seu tamanho definido e valores `3`, `5` e os demais como `0`.

```cpp
int casas [] {1,6,14,26,35};
```
↳ Inicializa array com seus valores definidos, tamanho é definido automáticamente.

**Acessando elementos na array:**
```html
<nome> [<n_elemento>];
```

**Exemplos:**
```cpp
casas [0];
```
↳ Seleciona o primeiro item da array `casas[]`.

#### Arrays multidimensionais:
Tem as mesmas caracteristicas de um array comum, porém possui 2 ou mais dimensões.

**Declarando array:**
```html
<tipo> <nome> [<tamanho>][<tamanho>]...;
```

#### Array 2D
<img src="https://https://github.com/pedcravo/Wiki/blob/main/C%2B%2B/2Darray.png" width="600px">

```cpp
const int Row (4);
const int Col (4);
int Arr [linhas][colunas];
```
↳ Apenas declara array 2D e define seu tamanho.

```cpp
const int Row (4);
const int Col (4);
int Arr [linhas][colunas]
{
  { 0, 4, 3, 5 },
  { 2, 1, 3, 5 },
  { 1, 2, 4, 5 },
  { 3, 1, 2, 5 },
};
```
↳ Declara a array 2D, define seu tamanho e valores.

**Acessando elementos na array:**
```html
<nome> [<n_elemento>][<n_elemento>]
  {
    {}, ...
  };
```

**Exemplos:**
```cpp
cin >> Arr[1][2];
```
↳ Insere dados do teclado a array.

```cpp
cout << Arr[1][2];
```
↳ Mostrta dados da array.

### Vetores
Os vetores são semelhantes as arrays, porém sua principal diferença é que os vetores não possuem tamanhos fixos.

Os vetores são mais versateis e mais manipulaveis, tendo funções como `sort`, `reverse`, `find` e mais.

**Declarando vetores:**
```html
# include <vector>

std::vector <<tipo>> <nome> (<tamanho>) {<valores>};
```

**Exemplos:**
```cpp
std::vector <int> notas (10);
```
↳ Declara vetor e define tamanho.

```cpp
std::vector <char> vowels (5);
```
↳ Declara vetor e define tamanho.

```cpp
std::vector <char> vowels {'a', 'e', 'i', 'o', 'u' };
```
↳ Declara vetor e define valores armazenados, o tamanho é definido automáticamente.

```cpp
std::vector <double> hi_temperatures (365, 80.9);
```
↳ Declara vetor e define o tamanho como `365` e o valor default como `80.9`.

**Acessando elementos no vetor com método array**
```html
<nome> [<n_elemento>];
```

**Exemplos:**
```cpp
vowels [0];
```
↳ Seleciona o primeiro item da vetor `vowels[]`.

**Acessando elementos no vetor com método vetor**
```html
<nome>.at (<n_elemento>);
```

**Exemplos:**
```cpp
vowels.at (0);
```
↳ Seleciona o primeiro item da vetor `vowels()`.

**Adicionar elementos ao fim do vetor:**
```html
<nome>.push_back (<n_elemento>);
```

**Exemplos:**
```cpp
vowels.push_back (d);
```
↳ Adiciona um valor ao fim do vetor.

### Fluxos de entrada e saída
Comandos utilizados para realizar a saída e a entrada de dados no sistema.

**Comandos associados:**
- `cin` → Entrada padrão para o teclado, recebe dados do teclado.
- `cout` → Saída padrão de dados no prompt, mostra no prompt algum dado.
- `cerr` → Saída de erros padrão, mostra erros.
- `clog` → Saída dos logs padrão, mostra logs.
- `endl` → Pula linha no prompt (endl - end line, \n pode susbtitui-lo na saída).
- `<<` → Usa dados anteriores como argumentos para o comando/variável anterior (geralmente anda junto com `cout`).
- `>>` → Usa dados anteriores para o comando/variável a seguir.

**Exemplos:**
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
  > A entrada de dados pode falhar dependendo da entrada e do tipo de dado solicitado (*int* recebe *string*).

### Estruturas
As estruturas são partes essenciais nos programas, pois através delas é possível escrever algoritmos.

São comuns e de sintaxe semelhantes na maioria das linguagens, bem como em c++.

#### Estruturas de Sequência
As estruturas de sequência são estruturas que organizam a sequencia a ser seguida na execução do código.

#### Estruturas de Seleção - Condicionais
As estruturas de seleção são as estruturas responsáveis por tomar decisões com base no restante do código. Elas que mudam o curso do código.

As principais são:
- `if` → Se for ***true*** executa `if`.
- `if-else` → Se for ***true*** executa `if` se ***false*** executa `else`.
- `if` encadeado → Encadeia diversos `if` onde todos precisam ser ***true***.
- `switch` → Uma série de casos para possíveis acontecimentos.
- `?` Condicional → `if-else` versão de operador, **operador ternário**.

##### IF
```cpp
if ('condition')
{
    /* code */
}
```

##### IF-ELSE
```cpp
if (condition)
{
    /* code */
}
else
{
    /* code */
}
```

##### IF-ELSEIF-ELSE
```cpp
if (condition)
{
    /* code */
}
else if (condition)
{
    /* code */
}
else
{
    /* code */
}
```

##### IF (encadeado)
```cpp
if (condition)
{
    if (condition)
    {
        /* code */
    }
}
```

##### SWITCH
```cpp
switch (expression)
{
case constant expression:
    /* code */
    break;

case constant expression:
    /* code */
    break;

default:
    /* code */
    break;
}
```

##### ? Condicional
```cpp
(cond_expr) ? expr1 : expr2
```


#### Estruturas de Iteração - Looping
As estruturas de iteração são estruturas que geram loops, que repetem uma parte do código até um determinado momento. Elas que repetem o código já executado.

As principais são:
- `for` → Loop que tem *início*, *condição de termino* e *incremento* bem definidos `(int i = 0; i < 100; i++)`.
- `while` → Loop que tem fim bem definido, não possui o início e nem como faz para ir ao fim.
- `do-while` → Loop que executa pelo menos 1 vez, tem fim bem definido semelhante ao `while`.

Os loops podem ser **Infinitos** caso mal implementados, geralmente tem um ponto para finalizar o loop e um meio de seguir até ele. É possível manipular os loops usando `continue` e `break`, evitando assim loops infinitos.

##### FOR
Este loop é especial pois tem *início*, *condição de termino* e *incremento* bem definidos em sua forma comum, porém é possível modifica-lo para se tornar infinito ou até mesmo para percorrer uma lista.

```cpp
for (size_t i = 0; i < count; i++)
{
    /* code */
}
```
↳ Loop `for` comum.

```cpp
for (;;)
{
    /* code */
}
```
↳ Loop `for` infinito.

```cpp
for (size_t i : sequence)
{
    /* code */
}
```
↳ Loop `for` que percorre sequencia.

##### WHILE
```cpp
while (condition)
{
    /* code */
}
```

##### DO-WHILE
```cpp
do
{
    /* code */
} while (condition);
```

# WIP
### Include
O include é um comando utilizado para importar bibliotecas e funções para seu código.

**As bibliotecas mais utilizadas:**
- `iostrem` →
- `fstream` →
- `string` →
- `string_view` →
- `vector` →
- `iomanip` →

#### rapidjson
Esta biblioteca é utilizada para transformar JSON em DOM e fazer o parse dos dados presentes nele.

[site do rapidjson →][rapidjson]

##### Estrutura e Comandos
A estrutura padrão do código é:
```cpp
#include "rapidjson/document.h"
 
using namespace rapidjson;

// Inserir JSON

Document document;
document.Parse(json);

// Codigo para manipular Parse do JSON
```

##### Verificar se um membro existe
```cpp
if (d.HasMember("chave")) { /* código */ }
```
- **O que faz?** Verifica se um determinado campo (chave) existe dentro do objeto JSON.
- **Exemplo:**
```cpp
Document d;
d.Parse(R"({ "nome": "Pedro" })");

if (d.HasMember("nome")) {
    std::cout << "Nome existe!\n";
}
```

##### Acessar um valor do JSON
```cpp
d["chave"]
```
- **O que faz?** Acessa o valor associado a uma chave dentro de um objeto JSON.
- **Exemplo:**
```cpp
Document d;
std::cout << d["nome"].GetString();  // Saída: Pedro
```
> **⚠️ IMPORTANTE:** Esse acesso assume que a chave já existe. Se a chave não existir, pode causar erro. Para evitar isso, use HasMember() antes.

##### Verificar o tipo de um valor
```cpp
d["chave"].IsString()
d["chave"].IsInt()
d["chave"].IsDouble()
d["chave"].IsBool()
d["chave"].IsArray()
d["chave"].IsObject()
```
- **O que faz?** Verifica se o valor de uma chave tem o tipo esperado.
- **Exemplo:**
```cpp
if (d["idade"].IsInt()) {
    std::cout << "Idade: " << d["idade"].GetInt();
}
```

##### Obter valores do JSON
```cpp
d["chave"].GetString() // Retorna uma string
d["chave"].GetInt()    // Retorna um inteiro
d["chave"].GetDouble() // Retorna um número decimal
d["chave"].GetBool()   // Retorna um booleano
```
- **O que faz?** Obtém o valor armazenado em uma chave específica.
- **Exemplo:**
```cpp
std::cout << "Nome: " << d["nome"].GetString();  // Saída: Nome: Pedro
std::cout << "Idade: " << d["idade"].GetInt();   // Saída: Idade: 25
```
> ⚠️ IMPORTANTE: Se o tipo do valor não for o esperado, o programa pode falhar. Verifique com IsXXX() antes.

##### Acessar elementos de um array
```cpp
const Value& array = d["numeros"];
for (SizeType i = 0; i < array.Size(); i++) {
    std::cout << array[i].GetInt() << " ";
}
```
- **O que faz?** Itera sobre um array JSON e acessa seus elementos.
- **Exemplo:**
```cpp
Document d;
d.Parse(R"({ "numeros": [10, 20, 30] })");

const Value& nums = d["numeros"];
for (SizeType i = 0; i < nums.Size(); i++) {
    std::cout << nums[i].GetInt() << " ";
}
// Saída: 10 20 30
```

##### Adicionar membros a um objeto JSON
```cpp
#include "rapidjson/writer.h"
#include "rapidjson/stringbuffer.h"

Document d;
d.SetObject();
Document::AllocatorType& allocator = d.GetAllocator();

d.AddMember("nome", "Pedro", allocator);
d.AddMember("idade", 25, allocator);
```
- **O que faz?** Adiciona novos campos ao JSON.

##### Adicionar elementos a um array

#### jsoncpp

#### glaze


```cpp
Value array(kArrayType);
Document::AllocatorType& allocator = d.GetAllocator();
array.PushBack(1, allocator).PushBack(2, allocator).PushBack(3, allocator);
```
- **O que faz?** Adiciona elementos a um array JSON.

### Funções
As funções são blocos de código que possuem nome e podem ser utilizadas em qualquer parte do código.

- `return` → É usado para retornar um valor (variável, constante e etc.) ao sistema ou a máquina, como: `return 0;`, `return a;`.

#### main()
A função `main()` é a principal função de qualquer software, pois ela que é executada ao inciar o programa.

Podemos ver a sintaxe padrão:
```cpp
int main()
{
  //codigo
  return 0;
}
```
Para executar este arquivo de código usamos:
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
Para executar este arquivo de código usamos:
```bash
$ programa.exe arg1 arg2
```

## Tipos de Erros
// WIP
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
Erros na lógica do programador, nenhum erro de escrita ou semântica, mas sim na lógica da escrita.
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
[rapidjson]: https://rapidjson.org/index.html