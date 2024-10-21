# Comandos de Ajuda no Linux
Nesta seção, exploramos comandos que fornecem ajuda sobre outros comandos no sistema Linux. Esses comandos são úteis para obter informações detalhadas sobre como utilizar outros comandos, suas opções e funcionalidades.

### Comandos:
1. [`help`](#1-help)
2. [`type`](#2-type)
3. [`man`](#3-man)
4. [`apropos`](#4-apropos)

---

## 1. `help`

### Para que serve?
Utilizado em conjunto com um comando para **exibir uma aba de ajuda sobre o comando definido**.
Mostra as opções disponíveis e uma breve descrição do que o comando faz, além de listar possíveis parâmetros que podem ser usados.

Na maioria dos casos, esse comando pode ser substituído por `-h`.

**Não é todo comando que `--help` pode ser utilizado.**

### Opções:
Não possui opções próprias, mas é aplicado com outros comandos como sendo uma opção deles.

### Sintaxe comum:
**`$ COMANDO --help`**

 ### Exemplos:
`$ help` → Mostra o manual geral do shell.

`$ ls --help` → Mostra aba de ajuda do comando `ls`.

`$ rmdir --help` → Mostra aba de ajuda do comando `rmdir`.

`$ apropos -h` → Mostra aba de ajuda do comando `apropos`.

### Máterial Complementar:
https://labex.io/tutorials/linux-get-help-on-linux-commands-18000

---

## 2. `type`

### Para que serve?
Utilizado para **descrever algum "nome" informado** como parâmetro, como comando **interno do bash, programa, função, palavra-chave, apelido** ou **arquivo**. Se nenhum nome for informado, ele não faz nada.

O comando `type` geralmente é usado para **descobrir as informações sobre um comando Linux**. Você pode descobrir facilmente qual o tipo do comando fornecido usando o comando `type`.
Além disso, você também pode encontrar o caminho real do comando.

### Opções:
`-a` → Mostra todas as informações do comando.

`-p` → Mostra local no sistema **(não mostra resultado para comandos)**.

`-P` → Mostra o caminho do executável.

`-t` → Mostra somente o tipo do comando.

### Sintaxe comum:
**`$ type [OPÇÃO] COMANDO`**

### Exemplos:
`$ type cd` → Mostra brevemente o que é o comando `cd`

`$ type ls` → Mostra brevemente o que é o comando `ls`.

`$ type ssh` → Mostra brevemente o que é o comando `ssh`.

`$ type -t ls` → Fala qual é o tipo do comando `ls`.

`$ type -p tree` → Mostra qual o local de `tree` no sistema.

`$ type -P pwd` → Mostra qual o caminho do executável do comando `pwd`.

`$ type -a tree` → Mostra todas as informações de `tree` no sistema.

### Máterial Complementar:
https://labex.io/tutorials/linux-get-help-on-linux-commands-18000

https://www.certificacaolinux.com.br/comando-linux-type/

https://www.bosontreinamentos.com.br/linux/certificacao-lpic-1/comando-type-ver-informacoes-sobre-outros-comandos-no-linux/#google_vignette

---
## 3. `man`

### Para que serve?
Utilizado para **acessar o manual de qualquer comando**.
O `man` é uma opção porém tem saída semelhante a saída de comandos, podendo ser contado e como um comando.
**(MANual)**

### Opções:
`-a` → Lista todos os manuais existentes sobre o tema.

`-k` → Pesquisa caracteres dentro do comando.

`N` → Escolhe manualmente a seção para entrar, sendo `N` o número da seção.

`-w` → Pesquisa o local do manual no sistema.

#### Dentro manual:
`↓↑` → Rola uma linha para cima ou para baixo.

`/termo` → Busca por "termo".

`n` → Pula para a próxima ocorrência da busca.

`N` → Pula para a próxima ocorrência da busca.

`space` → Avança uma página.

`b` → Volta uma página.

`q` → Sai do `man`.

### Sintaxe comum:
**`$ man [OPÇÕES] COMANDO`**

### Exemplos:
`$ man ls` → Mostra o manual do `ls`.

`$ man awk` → Mostra o manual do `awk`.

`$ man -k ls` → Pesquisa o comando `ls` dentro dos manuais.

`$ man -a intro` → Pesquisa todos os manuais relacionados ao comando `intro`.

`$ man 2 rmdir` → Entra na seção 2 do manual do comando `rmdir`.

`$ man -w rmdir` → Procura no sistema a localização do manual.

### Máterial Complementar:
https://labex.io/tutorials/linux-get-help-on-linux-commands-18000

https://www.baeldung.com/linux/man-command

---

## 4. `apropos`

### Para que serve?
Utilizado para **pesquisar palavras-chave nas descrições das páginas de manual** no sistema Linux.
O comando `apropos` ajuda a encontrar comandos e suas descrições associadas que correspondem a uma determinada palavra ou expressão regular, exibindo os resultados relevantes encontrados no `man`.

**É muito útil quando você sabe o que um comando faz, mas não lembra o nome exato dele, permitindo pesquisar por funções ou termos relacionados.**

### Opções:
`-a` → Exibe resultados que correspondam a todas as palavras-chave fornecidas.

`-e` → Busca exata. Procura pela palavra-chave exatamente como ela foi digitada, correspondendo ao nome completo ou descrição.

`-l` → Evita que a saída seja cortada para se ajustar à largura do terminal.

`-r` → Interpreta a palavra-chave como uma expressão regular (configuração padrão).

`-s N` → Pesquisa em seções específicas do manual, seções de número `N`.

`-v` → Modo detalhado, exibe mais informações durante a execução, útil para depuração.

`-w` → Interpreta a palavra-chave como um padrão com curingas (`?`, `*`)

### Sintaxe comum:
$ apropos [OPÇÕES] PALAVRA-CHAVE

### Exemplos:
`$ apropos find` → Procura o termo `find` pelas descrições de páginas de manuais.

`$ apropos -a -l find` → Procura pelas descrições de páginas de manuais que tenham pelo menos uma das letras do termo `find`, ignorando o tamanho do prompt.

`$ apropos -e find` → Mostra resultados onde o termo `find` corresponde exatamente à descrição ou ao nome.

`$ apropos -r find` → Pesquisa por todas as descrições de manual que contenham o termo `find` como parte de uma expressão regular.

`$ apropos -s 2 find` → Pesquisa apenas na seção 2 do manual.

`$ apropos -w "find*"` → Encontra apenas descrições que começam com `find`.

### Máterial Complementar:

https://labex.io/tutorials/linux-get-help-on-linux-commands-18000

https://www.linuxforce.com.br/comandos-linux/comandos-linux-comando-apropos/

https://guialinux.uniriotec.br/apropos/
