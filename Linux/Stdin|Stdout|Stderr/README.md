# Redirecionamento de Entradas e Saídas

Nesta sessão iremos ver as principais formas de redirecionar a saída de comandos: **Stdin** (Redirecionador de entrada), **Stdout** (Redirecionador de Saída Padrão) e **Stderr** (Redirecionador de Saída Erro).

### Comandos:
1. [`<`](#-redirecionador-de-entrada)
2. [`>` ou `1>`](#-ou-1-redirecionamento-de-saída-padrão)
3. [`>>` ou `1>>`](#-ou-1-redirecionamento-de-saída)
4. [`|`](#-redirecionamento-de-saída-de-comandos)
5. [`tee`](#tee)
6. [`2>`](#2-redirecionamento-de-saída-erro-padrão)
7. [`2>>`](#2-redirecionamento-de-saída-erro)
8. [`xargs`](#xargs)

## `<` (Redirecionador de Entrada)
### Para que serve?
O operador `<` no Linux é usado para r**edirecionar a entrada padrão de um comando.** Normalmente, um programa recebe entrada do teclado (`stdin`), mas com `<`, é possível direcioná-lo para ler a entrada de um arquivo.

> Isso é útil para automatizar comandos que precisam de entrada sem intervenção manual, lendo dados diretamente de arquivos.

### Sintaxe comum:
**`$ COMANDO < ARQUIVO`**

### Exemplos:
`$ cat < exemplo.txt` → Exibe o conteúdo do arquivo *exemplo.txt*, equivalente a `cat exemplo.txt`.

`$ sort < nomes.txt`→ Ordena alfabeticamente os nomes contidos em *nomes.txt*.

`$ wc < texto.txt` → Conta o número de linhas, palavras e caracteres no arquivo *texto.txt*.

```bash
$ ls > lista_arquivos.txt
$ sort < lista_arquivos.txt
```
→ O primeiro comando cria um arquivo com a saída de ls, o segundo ordena essa saída.

`$ cp <(grep $(whoami) /etc/passwd) myline` → Faz uma pesquisa utilizando `grep` e utiliza o arquivo temporário resultante deste comando como argumento para `cp`.

### Máterial Complementar:
https://ryanstutorials.net/linuxtutorial/piping.php#piping

https://labex.io/tutorials/linux-logical-commands-and-redirection-387332

---

## `>` ou `1>` (Redirecionamento de Saída Padrão)
### Para que serve?
Utilizado para **redirecionar a saída padrão para um arquivo ou shell**.
Caso o arquivo não exista, ele o cria.

> Sobrescreve o arquivo

### Sintaxe comum:
**`$ COMANDO > ARQUIVO/SHELL`**

### Exemplos:
`$ echo 'Eu terminei o projeto em $(date)' > projeto.txt` → Cria um arquivo projeto.txt com a frase *“Eu terminei o projeto”* ou sobrescreve caso já exista o arquivo.

`$ ls b*a > texte.txt` → Encontra todos os itens do diretório que começam com a letra *“B”* e terminam com a letra *“A”*, cria um arquivo teste.txt  e joga o que foi encontrado dentro do arquivo ou sobrescreve caso já exista.

`$ rmdir dir && echo "Diretório apagado" > /dev/pts/1` → Remove diretório e caso comando seja executado emite um echo no terminal */dev/pts/1*.

### Máterial Complementar:
<img src="https://github.com/pedcravo/Wiki/blob/main/Linux/RedirecionamentoSaida.webp" width="600px">

<img src="https://github.com/pedcravo/Wiki/blob/main/Linux/RedirecionamentoSaida.png" width="600px">

https://ryanstutorials.net/linuxtutorial/piping.php#piping

https://labex.io/tutorials/linux-logical-commands-and-redirection-387332

---

## `>>` ou `1>>` (Redirecionamento de Saída)
### Para que serve?
Utilizado para r**edirecionar a saída padrão para um arquivo ou shell.**
Caso o arquivo não exista, ele o cria.

> Atualiza o arquivo, concatena nele.

### Sintaxe comum:
**`$ COMANDO >> ARQUIVO/SHELL`**

### Exemplos:
`$ echo 'Eu terminei o projeto em $(date)' > projeto.txt` → Cria um arquivo *projeto.txt* com a frase *“Eu terminei o projeto”* ou adiciona ao arquivo caso já exista o mesmo já exista.

`$ ls a*o >> texte.txt` → Encontra todos os itens do diretório que começam com a letra *“A”* e terminam com a letra *“O”*, cria um arquivo *teste.txt* e joga o que foi encontrado dentro do arquivo ou adiciona caso já exista.

### Máterial Complementar:
<img src="https://github.com/pedcravo/Wiki/blob/main/Linux/RedirecionamentoSaida.png" width="600px">

https://labex.io/tutorials/linux-logical-commands-and-redirection-387332

---

## `|` (Redirecionamento de Saída de Comandos)
### Para que serve?
Utilizado para **direcionar saída de comandos para entrada de outros.**

> O resultado do comando de um comando **(stdout)** é a entrada de outro **(stdin)**.

### Sintaxe comum:
**`$ COMANDO1 | COMANDO2 `**

### Exemplos:
`$ tail -f /var/log/syslog | less` → Mostra utilizando o `less` os o arquivo em crescimento constante.

`$ ps aux | less` → Lista de forma detalhada as informações por intermédio do `less`.

`$ ps aux | grep ssh` → Lista de forma detalhada as informações e filtra elas utilizando o `grep` (filtra as palavras com *ssh*).

`$ ls | grep .txt` → Mostra os arquivos com o `ls` e filtra somente os que tem *.txt* com o `grep`.

`$ wc -c /var/log/syslog | awk '{print $1}' | numfmt --to=iec` → Conta a quantidade de bytes em */var/log/syslog*, filtra somente a primeira coluna e em seguida formata os números em Mb.

### Máterial Complementar:
<img src="https://github.com/pedcravo/Wiki/blob/main/Linux/RedirecionamentoSaida.webp" width="600px">

https://ryanstutorials.net/linuxtutorial/piping.php#piping

https://labex.io/tutorials/linux-logical-commands-and-redirection-387332

---

## `tee`
### Para que serve?
Utilizado para **dividir a saída do comando anterior**, uma sendo gravada em um arquivo e outra levada ao próximo arquivo.

### Sintaxe comum:
**`$ COMANDO | tee ARQUIVO | COMANDO`**

### Exemplos:
`$ ls -l | tee arquivo.txt | less` → Grava a saída do comando `ls` em um arquivo e em seguida o exibe na tela em forma paginada.

### Máterial Complementar:
<img src="https://github.com/pedcravo/Wiki/blob/main/Linux/tee.webp" width="600px">

---

## `2>` (Redirecionamento de Saída Erro Padrão)
### Para que serve?
Utilizado para **redirecionar a saída de erro** para um arquivo ou shell, não aparece na linha de comando a saída.

Caso o arquivo não exista, ele o cria.

> Sobrescreve o arquivo

### Sintaxe comum:
**`$ COMANDO 2> ARQUIVO/SHELL`**

### Exemplos:
`$ ls -@ 2> arquivo.txt` → Executa o comando e caso de erro *(comando está errado)* cria arquivo e armazena nele a saída de erro.

`$ find / -name "*US.dic" 2> /dev/null` → Procura usando `find` arquivos com o nome terminado em *US.dic*, as mensagens de erro envia para */dev/null* **(limbo do computador)**.

### Máterial Complementar:
<img src="https://github.com/pedcravo/Wiki/blob/main/Linux/RedirecionamentoSaida.png" width="600px">

https://labex.io/tutorials/linux-logical-commands-and-redirection-387332

---

## `2>>` (Redirecionamento de Saída Erro)
### Para que serve?
Utilizado para **redirecionar a saída de erro** para um arquivo ou shell, não mostra a saída na tela.

Caso o arquivo não exista, ele o cria.

> Atualiza o arquivo, não o sobrescreve.

### Sintaxe comum:
**`$ COMANDO 2>> ARQUIVO/SHELL`**

### Máterial Complementar:
<img src="https://github.com/pedcravo/Wiki/blob/main/Linux/RedirecionamentoSaida.png" width="600px">

https://labex.io/tutorials/linux-logical-commands-and-redirection-387332

---

## `xargs`
### Para que serve?
O comando `xargs` é utilizado para **executar comandos ou programas, utilizando como argumentos entrada padrão.** Esse comando é interessante para automatizar tarefas.

O `xargs` lê itens da entrada padrão, delimitados por espaços em branco ou novas linhas e executa o comando (o comando padrão é echo) uma ou mais vezes com quaisquer argumentos iniciais seguidos por itens lidos da entrada padrão. Linhas em branco na entrada padrão são ignoradas.

### Opções:
- `-0` → Interpreta a entrada com terminador nulo ao invés de espaços em branco (compatível com `find -print0` para nomes de arquivos com espaços).
- `-a ARQUIVO` → Lê a entrada de um `ARQUIVO` específico, em vez da entrada padrão.
- `-I REPLACE_STR` → Substitui a ocorrência da string `REPLACE_STR` no comando especificado pela entrada fornecida pelo `xargs`.
- `-L N` → Processa `N` linhas de entrada de uma vez, aplicando o comando a cada grupo de `N` itens.
- `-n N` → Limita o número de argumentos enviados ao comando por vez. Por padrão, `xargs` envia todos os argumentos de uma vez.
- `-p` → Pede confirmação antes de executar cada comando.
- `-t` → Exibe o comando antes de executá-lo, útil para verificar o que será executado.

### Sintaxe comum:
**`xargs [OPÇÕES] COMANDO ARGUMENTOS`**

### Exemplos:
`$ ls | xargs echo` → Mostra o resultado do comando `ls` em uma linha (elementos separados por um espaço.

`$ cat supermercado | xargs echo` → Mostra na tela o comando echo e em seguida tudo que há no arquivo supermercado.

`$ cat employees | xargs -t mkdir` → Cria um diretório com o nome de cada palavra do arquivo *employees* e mostra o comando `mkdir` juntamente com cada palavra do arquivo.

`$ cat employees | xargs rmdir` → Remove um diretório com o nome de cada palavra do arquivo *employees*.

`$ find . -name "*.log" -print0 | xargs -0 rm` → Encontra e remove arquivos *.log* utilizando o delimitador `-0` para nomes de arquivos com espaços ou caracteres especiais.

`$ find /origem -name "*.txt" | xargs -I {} cp {} /destino/` → Copia cada arquivo *.txt* encontrado para o diretório */destino*.

`$ echo "1 2 3 4 5" | xargs -n 2` → Divide a execução para enviar dois números ao comando de cada vez.

### Máterial Complementar:
https://www.certificacaolinux.com.br/comando-linux-xargs/