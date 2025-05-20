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
    - [Estruturas de Dados](#estruturas-de-dados)
      - [Array](#array)
        - [Create (Criar)](#create-criar)
        - [Read (Ler)](#read-ler)
        - [Update (Atualizar)](#update-atualizar)
        - [Delete (Excluir)](#delete-excluir)
      - [Arrays Multidimensionais](#arrays-multidimensionais)
        - [Create (Criar)](#create-criar-1)
        - [Read (Ler)](#read-ler-1)
        - [Update (Atualizar)](#update-atualizar-1)
        - [Delete (Excluir)](#delete-excluir-1)
      - [Vector](#vector)
        - [Create (Criar)](#create-criar-2)
        - [Read (Ler)](#read-ler-2)
        - [Update (Atualizar)](#update-atualizar-2)
        - [Delete (Excluir)](#delete-excluir-2)
      - [Vetores Multidimensionais](#vetores-multidimensionais)
        - [Create (Criar)](#create-criar-3)
        - [Read (Ler)](#read-ler-3)
        - [Update (Atualizar)](#update-atualizar-3)
        - [Delete (Excluir)](#delete-excluir-3)
      - [Struct](#struct)
        - [Create (Criar)](#create-criar-4)
        - [Read (Ler)](#read-ler-4)
        - [Update (Atualizar)](#update-atualizar-4)
        - [Delete (Excluir)](#delete-excluir-4)
      - [Vetor de Struct](#vetor-de-struct)
        - [Create (Criar)](#create-criar-5)
        - [Read (Ler)](#read-ler-5)
        - [Update (Atualizar)](#update-atualizar-5)
        - [Delete (Excluir)](#delete-excluir-5)
      - [Map](#map)
        - [Create (Criar)](#create-criar-6)
        - [Read (Ler)](#read-ler-6)
        - [Update (Atualizar)](#update-atualizar-6)
        - [Delete (Excluir)](#delete-excluir-6)
      - [Unordered Map](#unordered-map)
        - [Create (Criar)](#create-criar-7)
        - [Read (Ler)](#read-ler-7)
        - [Update (Atualizar)](#update-atualizar-7)
        - [Delete (Excluir)](#delete-excluir-7)
      - [Queue](#queue)
        - [Create (Criar)](#create-criar-8)
        - [Read (Ler)](#read-ler-8)
        - [Update (Atualizar)](#update-atualizar-8)
        - [Delete (Excluir)](#delete-excluir-8)
    - [Fluxos de entrada e saída](#fluxos-de-entrada-e-saída)
    - [Estruturas de Sequencia, Seleção e Iteração](#estruturas-de-sequencia-seleção-e-iteração)
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
    - [Bibliotecas](#bibliotecas)
    - [Funções](#funções)
      - [main()](#main)
    - [APIs](#apis)
      - [Entendendo a Pistache API em C++](#entendendo-a-pistache-api-em-c)
        - [O que é a Pistache API?](#o-que-é-a-pistache-api)
        - [Como Funciona a Pistache API?](#como-funciona-a-pistache-api)
        - [Exemplo Prático: Criando uma API REST Simples com Pistache](#exemplo-prático-criando-uma-api-rest-simples-com-pistache)
      - [Como Instalar e Configurar a Pistache](#como-instalar-e-configurar-a-pistache)
      - [Principais Características da Pistache](#principais-características-da-pistache)
      - [Exemplo Avançado: Manipulando JSON e POST](#exemplo-avançado-manipulando-json-e-post)
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
 
---

### Estruturas de Dados
As estruturas de dados são formas de organizar e armazenar dados na memória para facilitar operações como inserção, leitura, atualização e exclusão. Em C++, a biblioteca padrão (`STL - Standard Template Library`) oferece estruturas como `std::vector`, `std::map`, `std::queue`, entre outras, além de permitir a criação de estruturas personalizadas, como `struct`. Nesta seção, abordaremos as principais estruturas de dados, com foco nas operações **CRUD** (Create, Read, Update, Delete), suas características, declarações e exemplos práticos.

#### Array
Os **arrays** são estruturas estáticas que armazenam elementos do mesmo tipo em memória contígua, com tamanho fixo definido em tempo de compilação. São úteis quando o número de elementos é conhecido e não mudará.

**Características:**
- Tamanho fixo, definido na declaração.
- Armazenamento contíguo, permitindo acesso rápido via índices (O(1)).
- Todos os elementos devem ser do mesmo tipo (ex.: `int`, `float`).
- Não suporta operações dinâmicas como redimensionamento.
- Os elementos podem ser acessados diretamente e individualmente;
- O primeiro elemento tem índice 0, e o último tem índice `n-1`.

**Declaração de arrays:**
```html
<tipo> <nome>[<tamanho>] = {<valores>};
```

**Exemplo:**
```cpp
int notas[5] = {10, 7, 2, 8, 9}; // Array de 5 inteiros
```

**Operações CRUD em Arrays:**
Devido ao tamanho fixo, as operações CRUD em arrays são limitadas. Não há inserção ou exclusão verdadeira, mas podemos simular essas operações.

##### Create (Criar)
Define valores na declaração ou atribui valores a índices específicos.

**Exemplo:**
```cpp
int my_array[3];
my_array[0] = 10;
my_array[1] = 20;
my_array[2] = 30;
```

**Funcionamento:**
- A inicialização na declaração **ou** atribuição por índice é O(1).
- Após criação: `my_array = [10, 20, 30]`.

##### Read (Ler)
Acessa elementos por índice ou itera pelo array.

**Exemplo:**
```cpp
std::cout << "Elemento na posição 1: " << my_array[1] << std::endl; // Exibe 20
for (int i = 0; i < 3; i++) {
    std::cout << my_array[i] << " "; // Exibe 10 20 30
}
std::cout << std::endl;
```

**Funcionamento:**
- Acesso por índice é O(1).
- Iteração é O(n).

##### Update (Atualizar)
Modifica um elemento em um índice específico.

**Exemplo:**
```cpp
my_array[1] = 25; // Substitui 20 por 25
```

**Funcionamento:**
- Atualização por índice é O(1).
- Após atualização: `my_array = [10, 25, 30]`.

##### Delete (Excluir)
Não é possível remover elementos de um array (tamanho fixo). Pode-se "simular" a exclusão marcando o elemento como inválido (ex.: definindo como 0 ou outro valor sentinela) ou ignorando-o.

**Exemplo:**
```cpp
my_array[0] = 0; // "Remove" o elemento na posição 0 (marca como 0)
```

**Funcionamento:**
- Não há exclusão real; a marcação é O(1).
- Após "exclusão": `my_array = [0, 25, 30]`, mas o tamanho permanece 3.

**Cuidados:**
- Sempre valide índices para evitar acesso fora dos limites, que causa comportamento indefinido.
- Arrays são menos flexíveis que `std::vector` devido ao tamanho fixo.

**Exemplo Completo:**

Código contido no arquivo [type1.cpp](https://github.com/pedcravo/Praticando-Cpp/blob/main/Data-Types/type1.cpp)


#### Arrays Multidimensionais
Os **arrays multidimensionais** em C++ são estruturas estáticas que armazenam elementos do mesmo tipo em uma grade de múltiplas dimensões (ex.: matrizes 2D, 3D). São alocados em memória contígua e têm tamanho fixo definido em tempo de compilação.

**Características:**
- Tamanho fixo, definido na declaração.
- Armazenamento contíguo, com acesso por índices em O(1).
- Todos os elementos devem ser do mesmo tipo.
- Ideal para dados com dimensões conhecidas e imutáveis.

**Declaração de Arrays Multidimensionais:**
```html
<tipo> <nome>[<tamanho1>][<tamanho2>][...];
```

**Exemplo:**
```cpp
int matriz[2][3] = {{1, 2, 3}, {4, 5, 6}}; // Matriz 2x3 inicializada
```

**Operações CRUD em Arrays Multidimensionais:**
As operações CRUD (Create, Read, Update, Delete) são realizadas diretamente nos elementos via índices.

##### Create (Criar)
Inicializa o array com valores na declaração ou atribuição manual.

**Exemplo:**
```cpp
int matriz[2][3];
matriz[0][0] = 1; matriz[0][1] = 2; matriz[0][2] = 3;
matriz[1][0] = 4; matriz[1][1] = 5; matriz[1][2] = 6;
```

**Funcionamento:**
- Inicialização na declaração é O(1) por elemento.
- Após criação: `matriz = [[1, 2, 3], [4, 5, 6]]`.

##### Read (Ler)
Acessa elementos por índices ou itera pela matriz.

**Exemplo:**
```cpp
std::cout << "Elemento [1][2]: " << matriz[1][2] << std::endl; // Exibe 6
for (int i = 0; i < 2; i++) {
    for (int j = 0; j < 3; j++) {
        std::cout << matriz[i][j] << " "; // Exibe 1 2 3 4 5 6
    }
}
std::cout << std::endl;
```

**Funcionamento:**
- Acesso por índice (`matriz[i][j]`) é O(1).
- Iteração completa é O(n*m) para uma matriz `n x m`.

##### Update (Atualizar)
Modifica um elemento em uma posição específica.

**Exemplo:**
```cpp
matriz[1][2] = 10; // Substitui 6 por 10
```

**Funcionamento:**
- Atualização é O(1).
- Após atualização: `matriz = [[1, 2, 3], [4, 5, 10]]`.

##### Delete (Excluir)
Não há exclusão direta em arrays estáticos; pode-se "limpar" definindo valores padrão (ex.: 0).

**Exemplo:**
```cpp
matriz[1][2] = 0; // "Remove" definindo 0
```

**Funcionamento:**
- Atribuição de valor padrão é O(1).
- Arrays estáticos não permitem redimensionamento ou remoção real de elementos.

**Cuidados:**
- Verifique limites dos índices para evitar acesso inválido (undefined behavior).
- Arrays estáticos não podem ser redimensionados; use vetores multidimensionais para flexibilidade.


#### Vector
Os **vetores** (`std::vector`) são estruturas dinâmicas que armazenam elementos do mesmo tipo em memória contígua, com tamanho ajustável em tempo de execução. São mais versáteis que arrays, suportando operações como inserção e exclusão.

**Características:**
- Tamanho dinâmico, ajustado com `push_back`, `pop_back`, `resize`, etc.
- Armazenamento contíguo, com acesso por índice em O(1).
- Suporte a métodos como `size()`, `empty()`, `front()`, `back()`, `erase()`.
- Todos os elementos devem ser do mesmo tipo.

**Declaração de vetores:**
```html
#include <vector>
std::vector<<tipo>> <nome>(<tamanho>, <valor_default>);
```

**Exemplo:**
```cpp
#include <vector>
std::vector<int> notas(3, 0); // Cria vetor com 3 elementos inicializados com 0
notas.push_back(10);          // Adiciona 10 ao final
```

**Operações CRUD em Vetores:**
As operações CRUD são bem definidas em `std::vector`, com métodos específicos para cada uma.

##### Create (Criar)
Adiciona elementos com `push_back` (ao final) ou `insert` (em uma posição específica).

**Exemplo:**
```cpp
std::vector<int> my_vector;
my_vector.push_back(10);
my_vector.push_back(20);
my_vector.insert(my_vector.begin() + 1, 15);
```

**Funcionamento:**
- `push_back`: O(1) amortizado.
- `insert`: O(n) devido ao deslocamento.
- Após inserção: `my_vector = [10, 15, 20]`.

##### Read (Ler)
Acessa elementos por índice ou itera pelo vetor.

**Exemplo:**
```cpp
std::cout << "Elemento na posição 1: " << my_vector[1] << std::endl; // Exibe 15
for (const int& value : my_vector) {
    std::cout << value << " "; // Exibe 10 15 20
}
std::cout << std::endl;
```

**Funcionamento:**
- Acesso por índice (`my_vector[i]` ou `at(i)`) é O(1).
- Iteração é O(n).
- `at(i)` lança exceção para índices inválidos.

##### Update (Atualizar)
Modifica um elemento em uma posição específica.

**Exemplo:**
```cpp
my_vector[1] = 25; // Substitui 15 por 25
```

**Funcionamento:**
- Atualização é O(1).
- Após atualização: `my_vector = [10, 25, 20]`.

##### Delete (Excluir)
Remove elementos com `erase` (por posição) ou `pop_back` (último elemento).

**Exemplo:**
```cpp
my_vector.erase(my_vector.begin()); // Remove 10
my_vector.pop_back(); // Remove 20
```

**Funcionamento:**
- `erase`: O(n) devido ao deslocamento.
- `pop_back`: O(1).
- Após exclusões: `my_vector = [25]`.

**Cuidados:**
- Verifique `size()` ou `empty()` antes de acessar/remover elementos.
- Exclusão no início/meio é custosa; considere `std::deque` ou `std::list` para esses casos.

**Exemplo Completo:**

Código contido no arquivo [type1.cpp](https://github.com/pedcravo/Praticando-Cpp/blob/main/Data-Types/type1.cpp)


#### Vetores Multidimensionais
Os **vetores multidimensionais** (`std::vector` aninhado) são estruturas dinâmicas que armazenam vetores de vetores, permitindo dimensões ajustáveis em tempo de execução. São mais flexíveis que arrays multidimensionais.

**Características:**
- Tamanho dinâmico, ajustado com `push_back`, `resize`, etc.
- Armazenamento contíguo por linha, com acesso por índice em O(1).
- Suporte a métodos como `size()`, `empty()`, `resize()`.
- Todos os elementos devem ser do mesmo tipo.

**Declaração de Vetores Multidimensionais:**
```html
#include <vector>
std::vector<std::vector<<tipo>>> <nome>(<tamanho1>, std::vector<<tipo>>(<tamanho2>, <valor_default>));
```

**Exemplo:**
```cpp
#include <vector>
std::vector<std::vector<int>> matriz(2, std::vector<int>(3, 0)); // Matriz 2x3 inicializada com 0
matriz[0][2] = 3; // Atribui 3 à posição [0][2]
```

**Operações CRUD em Vetores Multidimensionais:**
As operações CRUD são realizadas com métodos do `std::vector` para manipular linhas e elementos.

##### Create (Criar)
Adiciona linhas ou elementos com `push_back` ou inicialização direta.

**Exemplo:**
```cpp
std::vector<std::vector<int>> matriz;
matriz.push_back({1, 2, 3}); // Adiciona linha [1, 2, 3]
matriz.push_back({4, 5, 6}); // Adiciona linha [4, 5, 6]
```

**Funcionamento:**
- `push_back` para linhas: O(1) amortizado.
- Inicialização de vetores aninhados: O(n*m) para `n x m`.
- Após inserção: `matriz = [[1, 2, 3], [4, 5, 6]]`.

##### Read (Ler)
Acessa elementos por índices ou itera pela matriz.

**Exemplo:**
```cpp
std::cout << "Elemento [1][2]: " << matriz[1][2] << std::endl; // Exibe 6
for (const auto& linha : matriz) {
    for (const int& valor : linha) {
        std::cout << valor << " "; // Exibe 1 2 3 4 5 6
    }
}
std::cout << std::endl;
```

**Funcionamento:**
- Acesso por índice (`matriz[i][j]`) é O(1).
- Iteração completa é O(n*m) para uma matriz `n x m`.
- Use `at(i)` para verificação de índices.

##### Update (Atualizar)
Modifica um elemento em uma posição específica.

**Exemplo:**
```cpp
matriz[1][2] = 10; // Substitui 6 por 10
```

**Funcionamento:**
- Atualização é O(1).
- Após atualização: `matriz = [[1, 2, 3], [4, 5, 10]]`.

##### Delete (Excluir)
Remove linhas ou elementos com `erase` ou `pop_back`.

**Exemplo:**
```cpp
matriz.erase(matriz.begin()); // Remove a primeira linha
matriz[0].pop_back(); // Remove o último elemento da primeira linha
```

**Funcionamento:**
- `erase` para linhas: O(n) devido ao deslocamento.
- `pop_back` para elementos: O(1).
- Após exclusões: `matriz = [[4, 5]]`.

**Cuidados:**
- Verifique `size()` de cada dimensão antes de acessar/remover elementos.
- Exclusão de linhas/elementos é custosa (O(n)); considere outras estruturas para remoções frequentes.
- Evite índices inválidos usando `at()` ou verificações manuais.

**Exemplo Completo:**
```cpp
#include <iostream>
#include <vector>

int main() {
    // Criando vetor multidimensional
    std::vector<std::vector<int>> matriz(2, std::vector<int>(3, 0));
    matriz[0] = {1, 2, 3}; // Create
    matriz[1] = {4, 5, 6};

    // Lendo elementos
    std::cout << "Elemento [1][2]: " << matriz[1][2] << std::endl; // Read
    for (const auto& linha : matriz) {
        for (const int& valor : linha) {
            std::cout << valor << " ";
        }
    }
    std::cout << std::endl;

    // Atualizando elemento
    matriz[1][2] = 10; // Update

    // Excluindo linha
    matriz.erase(matriz.begin()); // Delete
    for (const auto& linha : matriz) {
        for (const int& valor : linha) {
            std::cout << valor << " ";
        }
    }
    std::cout << std::endl;

    return 0;
}
```


#### Struct
As **estruturas** (`struct`) em C++ são tipos de dados definidos pelo usuário que agrupam variáveis de diferentes tipos sob um único nome. São semelhantes às classes, mas com membros públicos por padrão, sendo ideais para representar registros ou coleções de dados relacionados.

**Características:**
- Agrupa variáveis de tipos distintos (ex.: `int`, `float`, `string`).
- Acesso aos membros via operador `.` (ou `->` para ponteiros).
- Suporta métodos, construtores e herança, como classes.
- Armazenamento contíguo na memória, garantindo eficiência.

**Declaração de Structs:**
```cpp
struct <NomeDaStruct> {
    <tipo1> <membro1>;
    <tipo2> <membro2>;
    // Outros membros e métodos
};
```

**Exemplo:**
```cpp
#include <string>
struct Aluno {
    std::string nome;
    int idade;
    float nota;
};
Aluno aluno1;              // Instanciação
aluno1.nome = "João";      // Atribuição
aluno1.idade = 20;
aluno1.nota = 8.5;
```

**Operações CRUD em Structs:**
As operações CRUD (Create, Read, Update, Delete) referem-se à manipulação de instâncias e seus membros.

##### Create (Criar)
Cria uma instância da struct, inicializando seus membros.

**Exemplo:**
```cpp
Aluno aluno2 = {"Maria", 19, 9.0}; // Inicialização direta
// Usando construtor
struct Aluno {
    std::string nome;
    int idade;
    float nota;
    Aluno(std::string n, int i, float nt) : nome(n), idade(i), nota(nt) {}
};
Aluno aluno3("Pedro", 21, 7.5);
```

**Funcionamento:**
- Inicialização pode ser direta, uniforme ou via construtores.
- O(1) para criação de instâncias automáticas; O(n) para inicialização em coleções.

##### Read (Ler)
Acessa os membros de uma instância.

**Exemplo:**
```cpp
std::cout << "Nome: " << aluno1.nome << ", Idade: " << aluno1.idade
          << ", Nota: " << aluno1.nota << std::endl;
// Para ponteiros
Aluno* ptr = &aluno1;
std::cout << ptr->nome;
```

**Funcionamento:**
- Acesso via `.` ou `->` é O(1).
- Iteração em coleções de structs (ex.: em `std::vector`) é O(n).

##### Update (Atualizar)
Modifica valores dos membros de uma instância.

**Exemplo:**
```cpp
aluno1.nota = 9.5; // Atualiza nota
```

**Funcionamento:**
- Atualização é O(1) por acessar diretamente o membro.
- Após atualização: `aluno1 = {"João", 20, 9.5}`.

##### Delete (Excluir)
Remove uma instância, geralmente por saída de escopo ou liberação de memória.

**Exemplo:**
```cpp
Aluno* aluno4 = new Aluno{"Ana", 22, 8.0}; // Alocação dinâmica
delete aluno4; // Libera memória
```

**Funcionamento:**
- Instâncias automáticas (stack) são destruídas ao sair do escopo (O(1)).
- Instâncias dinâmicas (heap) requerem `delete` (O(1)).
- Em vetores: `std::vector<Aluno> turma; turma.erase(turma.begin());` (O(n)).

**Cuidados:**
- Evite acessar membros de structs desalocadas (undefined behavior).
- Inicialize membros para evitar valores indefinidos.
- Para gerenciar várias instâncias, use `std::vector<Aluno>`.

**Exemplo Completo:**

Código contido no arquivo [type1.cpp](https://github.com/pedcravo/Praticando-Cpp/blob/main/Data-Types/type1.cpp)


#### Vetor de Struct
Um **vetor de structs** em C++ utiliza `std::vector` para armazenar múltiplas instâncias de uma estrutura (`struct`). Combina a flexibilidade do vetor dinâmico com a capacidade da struct de agrupar dados heterogêneos, permitindo gerenciar coleções de registros de forma eficiente.

**Características:**
- Usa `std::vector<NomeDaStruct>` para armazenar instâncias de uma struct.
- Suporta operações dinâmicas como inserção, exclusão e acesso por índice.
- Elementos são armazenados em memória contígua, com acesso em O(1).
- Cada elemento do vetor é uma instância completa da struct, contendo todos os seus membros.

**Declaração de Vetor de Structs:**
```cpp
#include <vector>
struct NomeDaStruct {
    <tipo1> <membro1>;
    <tipo2> <membro2>;
};
std::vector<NomeDaStruct> nomeVetor;
```

**Exemplo:**
```cpp
#include <vector>
#include <string>
struct STR_DATA {
    int id;
    std::string name;
};
std::vector<STR_DATA> my_data;
```

**Operações CRUD em Vetor de Structs:**
As operações CRUD (Create, Read, Update, Delete) são aplicadas ao vetor, manipulando instâncias da struct.

##### Create (Criar)
Adiciona uma nova instância da struct ao vetor, geralmente com `push_back`.

**Exemplo:**
```cpp
STR_DATA new_data = {1, "cachorro"};
my_data.push_back(new_data); // Adiciona ao vetor
std::cout << "Novo item adicionado ao vetor\n";
std::cout << "Tamanho atual: " << my_data.size() << std::endl;
```

**Funcionamento:**
- `push_back`: O(1) amortizado.
- Permite criar e adicionar structs inicializadas diretamente.
- Após inserção: `my_data = [{1, "cachorro"}]`.

##### Read (Ler)
Acessa e exibe os membros das structs no vetor, geralmente iterando com um loop.

**Exemplo:**
```cpp
for (const auto& data : my_data) {
    std::cout << "Dado atual / id: " << data.id << " / name: " << data.name << std::endl;
}
```

**Funcionamento:**
- Acesso por índice (`my_data[i]`) é O(1).
- Iteração completa é O(n), onde `n` é o tamanho do vetor.
- Usa referência (`const auto&`) para evitar cópias desnecessárias.

##### Update (Atualizar)
Modifica uma instância da struct em uma posição específica do vetor.

**Exemplo:**
```cpp
STR_DATA new_data = {2, "ornitorrinco"};
my_data[1] = new_data; // Atualiza a posição 1
```

**Funcionamento:**
- Atualização por índice é O(1).
- Substitui a struct inteira na posição especificada.
- Após atualização: `my_data[1] = {2, "ornitorrinco"}`.

##### Delete (Excluir)
Remove uma instância da struct do vetor, geralmente com `erase`.

**Exemplo:**
```cpp
for (auto it = my_data.begin(); it != my_data.end(); ++it) {
    if (it->id == 1) {
        my_data.erase(it);
        break; // Sai do loop após exclusão
    }
}
std::cout << "Tamanho atual: " << my_data.size() << std::endl;
```

**Funcionamento:**
- `erase`: O(n) devido ao deslocamento de elementos.
- Necessário verificar o índice ou condição para evitar acessos inválidos.
- Após exclusão, o vetor é ajustado, reduzindo seu tamanho.

**Cuidados:**
- Verifique `size()` ou `empty()` antes de acessar elementos.
- Exclusão por ID requer busca (O(n)); considere `std::map` para buscas frequentes por chave.
- Evite acessar structs após remoção para evitar comportamento indefinido.
- Use `break` após `erase` em loops para evitar iteração inválida.

**Exemplo Completo:**

Código contido no arquivo [type1.cpp](https://github.com/pedcravo/Praticando-Cpp/blob/main/Data-Types/type1.cpp)


#### Map
O **map** (`std::map`) é uma estrutura de chave-valor ordenada, onde cada chave é única e mapeia para um valor. Usa uma árvore binária balanceada (geralmente uma Red-Black Tree) para manter as chaves ordenadas.

**Características:**
- Chaves são únicas e ordenadas (por padrão, em ordem crescente).
- Acesso, inserção e exclusão têm complexidade O(log n).
- Ideal para buscas frequentes por chave ou iteração ordenada.
- Suporta qualquer tipo de chave e valor, desde que a chave seja comparável.

**Declaração de maps:**
```html
#include <map>
std::map<<tipo_chave>, <tipo_valor>> <nome>;
```

**Exemplo:**
```cpp
#include <map>
std::map<int, std::string> my_map;
my_map[1] = "um";
my_map[2] = "dois";
```

**Operações CRUD em Maps:**
As operações CRUD são baseadas nas chaves.

##### Create (Criar)
Adiciona um par chave-valor com `insert` ou operador `[]`.

**Exemplo:**
```cpp
std::map<int, std::string> my_map;
my_map.insert({1, "um"});
my_map[2] = "dois"; // Insere ou atualiza
```

**Funcionamento:**
- `insert`: O(log n).
- `[]`: O(log n); insere se a chave não existe.
- Após inserção: `my_map = {1:"um", 2:"dois"}`.

##### Read (Ler)
Acessa valores por chave ou itera pelos pares.

**Exemplo:**
```cpp
std::cout << "Valor da chave 1: " << my_map[1] << std::endl; // Exibe "um"
for (const auto& pair : my_map) {
    std::cout << pair.first << ": " << pair.second << std::endl;
}
```

**Funcionamento:**
- Acesso por chave (`my_map[key]` ou `at(key)`) é O(log n).
- Iteração é O(n).
- `at(key)` lança exceção se a chave não existe.

##### Update (Atualizar)
Modifica o valor associado a uma chave.

**Exemplo:**
```cpp
my_map[1] = "one"; // Atualiza o valor da chave 1
```

**Funcionamento:**
- Atualização é O(log n).
- Após atualização: `my_map = {1:"one", 2:"dois"}`.

##### Delete (Excluir)
Remove um par chave-valor com `erase`.

**Exemplo:**
```cpp
my_map.erase(1); // Remove a chave 1
```

**Funcionamento:**
- `erase`: O(log n).
- Após exclusão: `my_map = {2:"dois"}`.

**Cuidados:**
- Verifique se a chave existe (`count(key)` ou `find(key)`) antes de acessar com `[]`, pois `[]` insere uma chave se ela não existe.
- Use `at(key)` para acesso seguro.

**Exemplo Completo:**
Código contido no arquivo [type2.cpp](https://github.com/pedcravo/Praticando-Cpp/blob/main/Data-Types/type2.cpp)


#### Unordered Map
O **unordered_map** (`std::unordered_map`) é uma estrutura de chave-valor não ordenada, implementada com uma tabela de hash, oferecendo acesso mais rápido que `std::map` em média.

**Características:**
- Chaves são únicas, mas não ordenadas.
- Acesso, inserção e exclusão têm complexidade O(1) em média (O(n) no pior caso).
- Ideal para buscas rápidas por chave.
- Usa mais memória que `std::map` devido à tabela de hash.

**Declaração de unordered_maps:**
```html
#include <unordered_map>
std::unordered_map<<tipo_chave>, <tipo_valor>> <nome>;
```

**Exemplo:**
```cpp
#include <unordered_map>
std::unordered_map<int, std::string> my_umap;
my_umap[1] = "um";
my_umap[2] = "dois";
```

**Operações CRUD em Unordered Maps:**
Semelhantes a `std::map`, mas com desempenho diferente.

##### Create (Criar)
Adiciona um par chave-valor.

**Exemplo:**
```cpp
std::unordered_map<int, std::string> my_umap;
my_umap.insert({1, "um"});
my_umap[2] = "dois";
```

**Funcionamento:**
- `insert` e `[]`: O(1) em média.
- Após inserção: `my_umap = {1:"um", 2:"dois"}`.

##### Read (Ler)
Acessa valores por chave ou itera pelos pares.

**Exemplo:**
```cpp
std::cout << "Valor da chave 1: " << my_umap[1] << std::endl; // Exibe "um"
for (const auto& pair : my_umap) {
    std::cout << pair.first << ": " << pair.second << std::endl;
}
```

**Funcionamento:**
- Acesso por chave é O(1) em média.
- Iteração é O(n).
- Ordem de iteração não é garantida.

##### Update (Atualizar)
Modifica o valor de uma chave.

**Exemplo:**
```cpp
my_umap[1] = "one";
```

**Funcionamento:**
- Atualização é O(1) em média.
- Após atualização: `my_umap = {1:"one", 2:"dois"}`.

##### Delete (Excluir)
Remove um par chave-valor.

**Exemplo:**
```cpp
my_umap.erase(1);
```

**Funcionamento:**
- `erase`: O(1) em média.
- Após exclusão: `my_umap = {2:"dois"}`.

**Cuidados:**
- Evite `[]` para leitura sem verificar a existência da chave.
- Performance pode degradar com muitas colisões na tabela de hash.

**Exemplo Completo:**
Código contido no arquivo [type3.cpp](https://github.com/pedcravo/Praticando-Cpp/blob/main/Data-Types/type3.cpp)


#### Queue
A **queue** (`std::queue`) é uma estrutura de fila que segue a política **FIFO** (First In, First Out). Elementos são inseridos no final e removidos do início.

**Características:**
- Suporta inserção no final (`push`) e remoção no início (`pop`).
- Acesso restrito ao primeiro (`front`) e último (`back`) elementos.
- Complexidade O(1) para inserção e remoção.
- Ideal para cenários como filas de tarefas ou buffers.

**Declaração de queues:**
```html
#include <queue>
std::queue<<tipo>> <nome>;
```

**Exemplo:**
```cpp
#include <queue>
std::queue<int> my_queue;
my_queue.push(10);
my_queue.push(20);
```

**Operações CRUD em Queues:**
As operações CRUD são limitadas devido à natureza FIFO.

##### Create (Criar)
Adiciona um elemento ao final com `push`.

**Exemplo:**
```cpp
std::queue<int> my_queue;
my_queue.push(10);
my_queue.push(20);
my_queue.push(30);
```

**Funcionamento:**
- `push`: O(1).
- Após inserção: `my_queue = [10, 20, 30]` (10 é o primeiro).

##### Read (Ler)
Acessa o primeiro (`front`) ou último (`back`) elemento.

**Exemplo:**
```cpp
std::cout << "Primeiro: " << my_queue.front() << std::endl; // Exibe 10
std::cout << "Último: " << my_queue.back() << std::endl; // Exibe 30
```

**Funcionamento:**
- `front` e `back`: O(1).
- Não há acesso direto a elementos intermediários.

##### Update (Atualizar)
Não há suporte direto para atualização, pois a queue não permite acesso arbitrário. Pode-se recriar a queue para simular.

**Exemplo (simulado):**
```cpp
std::queue<int> temp;
while (!my_queue.empty()) {
    int value = my_queue.front();
    my_queue.pop();
    if (value == 10) value = 15; // "Atualiza" 10 para 15
    temp.push(value);
}
my_queue = temp;
```

**Funcionamento:**
- Simulação é O(n).
- Após "atualização": `my_queue = [15, 20, 30]`.

##### Delete (Excluir)
Remove o primeiro elemento com `pop`.

**Exemplo:**
```cpp
my_queue.pop(); // Remove 10
```

**Funcionamento:**
- `pop`: O(1).
- Após exclusão: `my_queue = [20, 30]`.

**Cuidados:**
- Verifique `empty()` antes de acessar `front` ou `pop`.
- Não suporta exclusão arbitrária ou acesso a elementos intermediários.

**Exemplo Completo:**
Código contido no arquivo [type4.cpp](https://github.com/pedcravo/Praticando-Cpp/blob/main/Data-Types/type4.cpp)

---

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

---

### Estruturas de Sequencia, Seleção e Iteração
As estruturas Sequencia, Seleção e Iteração são partes essenciais nos programas, pois através delas é possível escrever algoritmos.

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

---

### Bibliotecas
O include é um comando utilizado para importar bibliotecas e funções para seu código.

**As bibliotecas mais utilizadas:**
- `iostrem` →
- `fstream` →
- `string` →
- `string_view` →
- `vector` →
- `map` →
- `unordered_map` →
- `queue` →
- `iomanip` →
- [`rapidjson`][rapidjson] → Mais veloz para parse de JSON.
- [`nlohmann`][nlohmann] → Escrita mais simples para parse de JSON.
- [`jsoncpp`][jsoncpp] → Mais detalhista para parse de JSON.
- [`glaze`][glaze] → Semelhante a velocidade da [rapidjson] e a escrita da [nlohmann] para parse de JSON, funciona melhor se tiver JSON padronizado.

---

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

### APIs
Anotações presentes no README da Wiki.

#### Entendendo a Pistache API em C++

A [**Pistache**](https://youtu.be/9BCO5W_Kw3Q?si=TxS6aYIThr9V3LKD) é um framework HTTP e REST de alta performance escrito em C++ (atualmente usando C++17), projetado para criar servidores e clientes HTTP com uma API clara e elegante. Ele é ideal para desenvolver APIs RESTful, oferecendo suporte a operações como GET, POST, e manipulação de respostas em formatos como JSON. A seguir, explico o que é a Pistache, como ela funciona, seus principais componentes e um exemplo prático, integrando os conceitos de APIs em C++ e informações específicas sobre a Pistache obtidas de fontes confiáveis.

##### O que é a Pistache API?
A Pistache é uma biblioteca open-source que fornece uma interface para construir servidores HTTP e APIs REST em C++. Ela é leve, multithreaded e usa um modelo assíncrono baseado em **promises** e **futures** para lidar com requisições de forma eficiente. Seu objetivo é simplificar a criação de serviços web robustos, com suporte a:

- **Servidores HTTP**: Para processar requisições GET, POST, PUT, DELETE, etc.
- **Clientes HTTP**: Para fazer chamadas a outros serviços.
- **Roteamento**: Para mapear URLs a funções específicas.
- **Manipulação de Dados**: Suporte a MIME types, JSON, e envio de arquivos estáticos.

A Pistache é compatível com Linux, macOS, Windows e sistemas BSD, embora algumas funcionalidades (como chamadas específicas do Linux, como `epoll`) limitem sua portabilidade total sem ajustes.
- [Reddit](https://www.reddit.com/r/cpp/comments/6ehhqe/has_anyone_tested_andor_reviewed_pistacheio_c/)
- [Github](https://github.com/pistacheio/pistache/blob/master/README.md)

##### Como Funciona a Pistache API?
A Pistache opera em torno de alguns conceitos centrais que permitem criar servidores e APIs REST de maneira eficiente:

1. **Http::Endpoint**:
   - Representa o servidor HTTP. É configurado com um endereço (IP e porta) e inicializado para escutar requisições.
   - Exemplo: `Http::Endpoint endpoint(Address("localhost", 8080));` cria um servidor na porta 8080.

2. **Http::Handler**:
   - Classes que herdam de `Http::Handler` definem como as requisições HTTP são processadas.
   - O método principal é `onRequest(const Http::Request& request, Http::ResponseWriter response)`, que recebe a requisição e envia a resposta.
   - Exemplo: Um handler pode responder "Hello, World" para uma requisição GET.

3. **Roteamento (Rest::Router)**:
   - Permite mapear URLs e métodos HTTP (GET, POST, etc.) a funções específicas.
   - Exemplo: `Routes::Get(router, "/hello", [](const Rest::Request&, Http::ResponseWriter response) {...});`.

4. **Modelo Assíncrono**:
   - A Pistache usa **promises** e **futures** para operações assíncronas, como envio de respostas ou leitura de arquivos, evitando bloqueios.[](https://pistacheio.github.io/pistache/docs/http-handler/)
   - Isso melhora a escalabilidade, mas foi criticado por alguns desenvolvedores em comparação com modelos baseados em callbacks (como o Boost.Asio), devido a possíveis overheads.[](https://www.reddit.com/r/cpp/comments/6ehhqe/has_anyone_tested_andor_reviewed_pistacheio_c/)

5. **Respostas e Requisições**:
   - **Http::Request**: Contém informações da requisição (método, URL, query parameters, body).
   - **Http::ResponseWriter**: Usado para enviar respostas, incluindo código HTTP (200, 404, etc.), corpo (como JSON) e cabeçalhos.
   - Suporta envio de arquivos estáticos (`Http::serveFile`) e respostas chunked para dados dinâmicos.[](https://pistacheio.github.io/pistache/docs/http-handler/)

6. **Multithreading**:
   - A Pistache é multithreaded por padrão, usando um número de threads baseado nos núcleos da CPU, o que a torna eficiente para lidar com múltiplas conexões simultâneas.[](https://reposhub.com/cpp/web-application-framework/oktal-pistache.html)

##### Exemplo Prático: Criando uma API REST Simples com Pistache
Aqui está um exemplo de como criar um servidor REST que responde a uma requisição GET na rota `/hello` com uma mensagem simples:

```cpp
#include <pistache/endpoint.h>
#include <pistache/router.h>
#include <pistache/http.h>

using namespace Pistache;

class HelloHandler : public Http::Handler {
public:
    HTTP_PROTOTYPE(HelloHandler)

    void onRequest(const Http::Request& request, Http::ResponseWriter response) override {
        response.send(Http::Code::Ok, "Hello, World!\n");
    }
};

void setupRoutes(Rest::Router& router) {
    Rest::Routes::Get(router, "/hello", [](const Rest::Request&, Http::ResponseWriter response) {
        response.send(Http::Code::Ok, "Hello from Router!\n");
        return Rest::Route::Result::Ok;
    });
}

int main() {
    // Configura o endpoint
    Address addr(Ip::any(), 8080);
    Http::Endpoint endpoint(addr);
    
    // Configura opções do servidor
    auto opts = Http::Endpoint::options().threads(4);
    endpoint.init(opts);

    // Configura roteamento
    Rest::Router router;
    setupRoutes(router);
    
    // Associa o router ao endpoint
    endpoint.setHandler(router.handler());

    // Inicia o servidor
    endpoint.serve();
    
    // Para o servidor graciosamente
    endpoint.shutdown();
    return 0;
}
```

**Explicação do Código**:
- **Http::Endpoint**: Configurado para escutar na porta 8080.
- **Rest::Router**: Define uma rota `/hello` que responde com uma mensagem.
- **Http::Handler**: Um handler personalizado pode ser usado para lógicas mais complexas.
- **Multithreading**: O servidor usa 4 threads para maior desempenho.
- **Resposta**: A rota `/hello` retorna o código HTTP 200 e a mensagem "Hello from Router!".

Para testar, compile o código (certifique-se de ter a Pistache instalada) e use `curl`:
```bash
curl http://localhost:8080/hello
# Resposta: Hello from Router!
```

#### Como Instalar e Configurar a Pistache
Para usar a Pistache, você precisa instalá-la e configurá-la no seu projeto. Aqui estão os passos básicos para um ambiente Linux (Ubuntu):

1. **Instalação via Pacotes Pré-compilados**:[](https://pistacheio.github.io/pistache/docs/)
   ```bash
   sudo add-apt-repository ppa:pistache+team/unstable
   sudo apt update
   sudo apt install libpistache-dev
   ```

2. **Compilação Manual**:
   ```bash
   git clone https://github.com/pistacheio/pistache.git
   cd pistache
   mkdir build
   cd build
   cmake -G "Unix Makefiles" -DCMAKE_BUILD_TYPE=Release ..
   make
   sudo make install
   ```

3. **Configuração no CMake**:
   Para integrar a Pistache ao seu projeto, ajuste o `CMakeLists.txt`:
   ```cmake
   cmake_minimum_required(VERSION 3.12)
   project(PistacheExample)
   set(CMAKE_CXX_STANDARD 17)
   find_package(Pistache REQUIRED)
   add_executable(${PROJECT_NAME} src/main.cpp)
   target_link_libraries(${PROJECT_NAME} Pistache::Pistache)
   ```
   Isso garante que os headers e bibliotecas da Pistache sejam incluídos corretamente.[](https://stackoverflow.com/questions/52468551/include-pistache-in-c-project)

#### Principais Características da Pistache
- **Alta Performance**: Usa chamadas de sistema eficientes (como `epoll` no Linux) e multithreading para lidar com muitas conexões.[](https://www.reddit.com/r/cpp/comments/6ehhqe/has_anyone_tested_andor_reviewed_pistacheio_c/)
- **API Elegante**: Oferece uma sintaxe clara para definir rotas e handlers.[](https://www.linuxlinks.com/pistache-modern-elegant-http-rest-framework/)
- **Suporte a JSON**: Embora não inclua parsing de JSON nativo (para manter a leveza), pode ser combinado com bibliotecas como RapidJSON.[](https://github.com/pistacheio/pistache/issues/211)
- **Assincronia**: Usa promises para operações como envio de respostas ou leitura de arquivos, ideal para APIs com baixa latência.[](https://pistacheio.github.io/pistache/docs/http-handler/)
- **Flexibilidade**: Suporta tanto servidores REST quanto clientes HTTP para chamadas externas.[](https://www.linuxlinks.com/pistache-modern-elegant-http-rest-framework/)


---

#### Exemplo Avançado: Manipulando JSON e POST
Para um caso mais realista, como um servidor que recebe um POST com JSON e retorna uma resposta manipulada:

```cpp
#include <pistache/endpoint.h>
#include <pistache/router.h>
#include <rapidjson/document.h>
#include <rapidjson/writer.h>
#include <rapidjson/stringbuffer.h>

using namespace Pistache;
using namespace rapidjson;

void handlePost(const Rest::Request& request, Http::ResponseWriter response) {
    // Obtém o corpo da requisição
    auto body = request.body();
    
    // Parsing do JSON
    Document doc;
    doc.Parse(body.c_str());
    
    if (!doc.IsObject() || !doc.HasMember("name")) {
        response.send(Http::Code::Bad_Request, "JSON inválido\n");
        return;
    }
    
    // Extrai o campo "name"
    auto name = doc["name"].GetString();
    
    // Cria uma resposta JSON
    StringBuffer buffer;
    Writer<StringBuffer> writer(buffer);
    writer.StartObject();
    writer.Key("message");
    writer.String(("Olá, " + std::string(name) + "!").c_str());
    writer.EndObject();
    
    response.headers().add<Http::Header::ContentType>(MIME(Application, Json));
    response.send(Http::Code::Ok, buffer.GetString());
}

int main() {
    Address addr(Ip::any(), 8080);
    Http::Endpoint endpoint(addr);
    auto opts = Http::Endpoint::options().threads(4);
    endpoint.init(opts);
    
    Rest::Router router;
    Rest::Routes::Post(router, "/greet", handlePost);
    
    endpoint.setHandler(router.handler());
    endpoint.serve();
    
    endpoint.shutdown();
    return 0;
}
```

**Explicação**:
- **RapidJSON**: Usado para parsear e criar JSON.
- **Rota POST**: A rota `/greet` aceita um POST com um JSON como `{"name": "Alice"}`.
- **Resposta**: Retorna um JSON como `{"message": "Olá, Alice!"}`.

**Teste com curl**:
```bash
curl -X POST -H "Content-Type: application/json" -d '{"name":"Alice"}' http://localhost:8080/greet
# Resposta: {"message":"Olá, Alice!"}
```

---

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

`g++-13` → Versão do compilador específica. Pode ser usada simplesmente como `g++`.

`-g -ggdb` → Torna o arquivo debugavel.

`-std=c++23` → Versão da linguagem.

`app.cpp` → Arquivo padrão.

`-o APP` → Renomeia o executável padrão para APP.

**`$ g++-13 -On -std=c++23 app2.cpp -o APP`** → Cria arquivo executável com flags de compilação.

`-On` → Flags de compilação, onde o `n` define a flag (`0` a `3`).

- `-O0` →

- `-O1` →

- `-O2` →

- `-O3` → Modo **Release**, modo mais veloz e otimizado do código.

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
[glaze]: glaze/
[jsoncpp]: jsoncpp/
[nlohmann]: nlohmann/
[rapidjson]: rapidjson/