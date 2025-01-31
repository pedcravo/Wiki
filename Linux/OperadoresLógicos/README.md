# Operadores Lógicos

Nesta sessão iremos ver os operadores lógicos que podem ser usados para encadear comandos.

### Operadores:

1. [`;`](#-após)
2. [`&&`](#-and)
3. [`||`](#-or)

## `;` (APÓS)

### Para que serve?
Utilizado para **encadear comandos, executa o comando seguinte independente do resultado dele.**

> Idependende do resultado do primeiro comando, **se foi bem ou mal sucedido**, o segundo é executado.

### Sintaxe comum:
**`$ COMANDO ; COMANDO`**

### Exemplos:
`$ git checkout teste; git log --oneline --graph; git checkout main` → Faz o checkout na branch teste, após isso mostra os commits com formatação própria e após isso faz checkout na main.

### Máterial Complementar:
https://labex.io/tutorials/linux-logical-commands-and-redirection-387332

---

## `&&` (AND)

### Para que serve?
Utilizado para **executar comandos seguidos, o comando da direita caso o da esquerda tenha sucesso.**

> Caso o primeiro comando foi **bem sucedido**, o segundo é executado.

### Sintaxe comum:
**`$ COMANDO1 && COMANDO2`**

### Exemplos:
`$ mkdir diretorio && echo "Comando bem sucedido, diretório criado"` → Cria um diretório, caso comando de certo executa o `echo`, mostra na tela *"Comando bem sucedido, diretório criado"*.

### Máterial Complementar:
https://labex.io/tutorials/linux-logical-commands-and-redirection-387332

---

## `||` (OR)

### Para que serve?
Utilizado para **executar comandos seguidos, o comando da direita caso o da esquerda tenha falhado**.

> Caso o primeiro comando foi **mal sucedido**, o segundo é executado.

### Sintaxe comum:
**`$ COMANDO1 || COMANDO2`**

### Exemplos:
`$ mkdir diretorio || echo "Falha ao criar o diretório"` → Cria um diretório, caso de erro ou comando não de certo executa o `echo`, mostra na tela "Falha ao criar o diretório".

### Máterial Complementar:
https://labex.io/tutorials/linux-logical-commands-and-redirection-387332