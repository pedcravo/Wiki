# C++
Nesta sessão vamos estudar sobre C++, seus conceitos, equações e prática.

Toda a parte prática vamos usar o diretório [Aprendendo C++][pratica].

## Tópicos:
- [C++](#c)
  - [Tópicos:](#tópicos)
  - [Conceitos](#conceitos)
    - [Variáveis:](#variáveis)
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

### Variáveis:

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

[pratica]: https://github.com/pedcravo/Aprendendo-C-
[compilador]: https://www.tutorialspoint.com/gnu_debugger/index.htm