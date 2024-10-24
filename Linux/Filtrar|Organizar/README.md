# Comandos para Filtrar e Organizar Dados

Nesta seção, exploramos comandos que permitem filtrar e organizar dados no Linux.
Estes comandos são amplamente utilizados para manipulação de texto e processamento de arquivos, permitindo operações como filtrar e recortar dados de forma flexível.

### Comandos:

1. [`cut`](#1-cut)
2. [`grep`](#2-grep)
3. [`awk`](#3-awk)
4. [`head`](#4-head)
5. [`tail`](#5-tail)
6. [`less`](#6-less)
7. [`nl`](#7-nl)
8. [`sort`](#8-sort)
9. [`tac`](#9-tac)
10. [`uniq`](#10-uniq)

## 1. `cut`

### Para que serve?
Utilizado para **filtrar os conteúdos dos arquivos** com base nos separadores, caracteres e até mesmo bytes do arquivo.

### Opções:
- `-b N` → Seleciona bytes pelo número `N`.
- `-c N` → Seleciona caracteres pelo número `N`.
- `-d` → Seleciona o separador, separador padrão `:`.
- `-fN,..` → Seleciona a coluna `N`.

### Sintaxe comum:
**`cut [OPÇÕES] ARQUIVO`**

### Exemplos:
`$ cut -b 20 arquivo.txt` → Mostra uma coluna somente com o byte 20 de cada linha do arquivo.

`$ cut -c 20 arquivo.txt` → Mostra uma coluna somente com o caractere número 20 de cada linha do arquivo.

`$ cut -d , -f1,3  arquivo2.txt` → Filtra as colunas 1 e 3 do arquivo separados pelo caractere _“,”_.

`$ cut -d , -f1  arquivo2.txt` → Filtra a coluna 1 do arquivo separado pelo caractere _“,”_.

### Máterial Complementar:
https://www.certificacaolinux.com.br/comando-linux-cut/

https://www.geeksforgeeks.org/cut-command-linux-examples/

---

## 2. `grep`

### Para que serve?
O grep (Global Regular Expression Print) é utilizado para **filtrar/pesquisar linhas com base em caracteres e palavras em um ou mais arquivos**.
Faz uso de Expressões Regulares e de [Meta Caracteres](../MetaCaractere/README.md).

#### Tem derivadas como:
- `egrep` → Utiliza **expressões regulares estendidas** como +, ?, {} ou |, sem a necessidade de usar \ antes do operador.
- `fgrep` → Procura o caractere como string e não como operador (., * e |).
- `lgrep` → Busca arquivos com suporte a expressões regulares (**no entanto, não faz parte dos comandos padrão de linha de comando em sistemas Linux**).

### Opções:
- `-A` → Mostra as linhas depois daquelas com o caractere.
- `-B` → Mostra as linhas antes daquelas com o caractere.
- `-c` →Conta a quantidade de vezes que a palavra aparece.
- `-e` → Pesquisa mais de uma palavra, mostra somente as linhas em que ambas estão inclusas.
- `-E`  ou `egrep` → Utiliza expressões regulares estendidas como +, ?, {} ou |, sem a necessidade de usar \ antes do operador.
- `-F`  ou `fgrep` → Procura o caractere como string e não como operador (., * e |).
- `lgrep` → busca arquivos com suporte a expressões regulares (no entanto, não faz parte dos comandos padrão de linha de comando em sistemas Linux).
- `-i` → Procura pela palavra não diferenciando entre maiúsculo e minusculo.
- `-l` → Mostra os nomes dos arquivos que contem o linhas com o caractere.
- `-n` → Mostra o número de cada linha ao lado das linhas.
- `-r`  ou `-R` → Pesquisa recursivamente nos subdiretórios.
- `-v` → Mostra as linhas que não contém o caractere.
- `-w` → Mostra somente as palavras completas.

#### Opções utilizadas frequentemente:
-ic ↔ -i + -c
-vi ↔ -v + -i
-ri ↔ -r + -i
-rli ↔ -r + -l + -i

### Sintaxe comum:
#### grep
**`$ grep [OPÇÕES] PALAVRA ARQUIVO`**

#### egrep
**`$ egrep [EXPRESÃO] ARQUIVO`**

#### fgrep
**`$ fgrep [EXPRESSÃO] ARQUIVO`**

### Exemplos:
#### grep
`$ grep idade arquivo.txt arquivo2.txt` - Mostra todas as linhs dos arquivos selecionados em que a palavra idade aparece.

`$ grep "database connection failed" logs/*` → Pesquisa em todos os arquivos do diretório `logs` a frase _"databese connection failed"_.

`$ grep -i o arquivo.txt` - Mostra as linhas do arquivo que tem o caractere _“o”_ (sozinho ou em uma palavra) não diferencia o maiúsculo do minusculo.

`$ grep -c lorem arquivo.txt` - Mostra o número total de linhas que combinam com _“lorem”_.

`$ grep -e bem -e pedro arquivo.txt` → Mostra somente as linhas que tem ambas as palavras na linha.

`$ grep -r l arquivo.txt` - Faz uma pesquisa recursiva procurando o caractere _“l”_.

`$ grep -v ipsum arquivo.txt` - Mostra as linhas que não tem o caractere _“ipsum”_.

`$ grep -B 2 -A 2 -i "1994-06-23 02:38:37" datas.txt` → Motra as 2 linhas antes e as 2 depois da data pesquisada.

`$ grep -n 40 datas.txt` → Mostra as linhas que tem o número _"40"_ e também mostra o número de sua linha ao lado.

`$ grep -n 40 datas.txt; grep -c 40 datas.txt` → Mostra as linhas que tem o número _"40"_, juntamente com o número de sua linha e em seguida mostra o total de linhas.

`$ grep -w "Maria" arquivo2.txt` → Pesquisa pela palavra _"Maria"_ no arquivo.

`$ grep ^bom arquivo.txt` → Mostra as linhas do arquivo que começam com a palavra _"bom"_.

`$ grep dia$ arquivo.txt`  → Mostra as linhas do arquivo que teminam com _"dia"_.

`$ grep dia > saida.txt` → Transforma a pesquisa em um arquivo `.txt` e não mostra na tela o resultado da busca.

#### egrep
`$ egrep "erro|falha" arquivo.txt` → Procura as linhas que tem as palavras _"erro"_ ou _"falha"_ (tem como equivalente `grep`: `$ grep "erro\|falha" arquivo.txt`).

`$ egrep "a.c" arquivo.txt` → procura por qualquer linha que tenha a sequencia _"a"_, seguido de qualquer caractere, seguido de _"c"_ (por exemplo, _"abc"_, _"a-c"_, _"a1c"_).

`$ egrep "colou?r" arquivo.txt` → Procura por _"color"_ ou _"colour"_ (o _"u"_ pode ou não estar presente).

`$ egrep "ca*r" arquivo.txt` → Procura por qualquer palavra que tenha 0 ou mais de _"a"_ entre _"c"_ e _"r"_.

`$ egrep "ca+r" arquivo.txt` → Procura por qualquer palavra que tenha 1 ou mais de _"a"_ entre _"c"_ e _"r"_.

`$ egrep "a{3}" arquivo.txt` → Procura pela letra _"a"_ se repetindo 3 vezes consecutivas.

`$ egrep "a{2,4}" arquivo.txt` → Procura pela letra _"a"_ se repetindo de 2 a 4 vezes consecutivas.

`$ egrep "[abc]" arquivo.txt` → Procura por qualquer ocorrência de _"a"_, _"b"_ ou _"c"_ em uma linha.

`$ egrep '[aeiou]{2,}' arquivo.txt` → Procura pelas linhas que tenham algum destes caracteres _"a"_, _"e"_, _"i"_, _"o"_ e _"u"_ aparecendo duas ou mais vezes.

`$ egrep "[^abc]" arquivo.txt` → Procura por qualquer linha que não tenha a ocorrencia de _"a"_, _"b"_ ou _"c"_.

`$ egrep "[c-f]" arquivo.txt` → Procura pelas linhas com qualquer um dos caracteres entre _"c"_ e _"f"_.

`$ egrep "(ab)+" arquivo.txt` → Procura por 1 ou mais ocorrências da sequência _"ab"_, como _"ab"_, _"abab"_, _"ababab”_.

#### fgrep
`$ fgrep "?" arquivo.txt` → Procura as linhas que tenham o caractere `?` ( tem como equivalente `grep`: `$ grep "\?" arquivo.txt`).

### Máterial Complementar:
https://www.hostinger.com.br/tutoriais/comando-grep-linux

https://labex.io/tutorials/linux-linux-grep-command-pattern-searching-219192

https://cloudminister.com/blog/how-to-use-grep-command-in-linux/

https://ryanstutorials.net/linuxtutorial/grep.php

https://github.com/BurntSushi/ripgrep

---

## 3. `awk`

### Para que serve?
Utilizado para **filtra, recortar, printar** e etc.

É semelhante ao `cut` + `grep`.

**É possível utilizar [Meta Caracteres](../MetaCaractere/README.md), funções Lambda, funções com string e etc**.

### Opções:
- `-F` → Tem como padrão para pesquisa o separador: _“:”_ mas pode ser alterado por _“,”_, _“.”_ dentre outros.

#### Tipos de seletores de caracteres:
- `$N` → Escolhe a coluna `N`.
- `$N,$M` → Escolhe as colunas `N` e `M`.
- `”palavra”` → Usado quando inserir string
- `BEGIN` → Usado para fazer uma ação ao começar a rodar.
- `END` → Usado para fazer uma ação depois que a anterior terminar (final).

### Sintaxe comum:
**`$ awk -F 'CARACTERE {print $NUMERO-DA-COLUNA}' ARQUIVO`**

### Exemplos:
`$ awk {print} arquivo.txt` → Imprime todas as linhas do arquivo.

`$ awk '{ print $0 }' arquivo.txt` → Imprime todas as linhas do arquivo.

`$ awk -F, '{print $1}' arquivo.txt` → Filtra as palavras semelhante ao `cut -df`.

`$ awk -F, '{print $1,$3}' arquivo.txt` → Filtra as palavras semelhante ao `cut -df`.

`$ awk -F, '/^n/{print $1,$3}' arquivo.txt` → Mostra somente as colunas 1 e 3 das linhas que tem o primeiro caractere _“n”_.

`$ awk { print "" } arquivo.txt` → Mostra _“ “_ no lugar de cada linha do arquivo.

`$ awk { print "hey" } arquivo.txt` → Mostra _“hey“_ no lugar de cada linha do arquivo.

`$ awk -F: '/\/bin\//{print $1,$7}' /etc/passwd` → Mostra somente os nomes (coluna 1) e interpretador (coluna 7) das linhas que tem o caminho `/bin/`.

`$ awk -F: ‘/^.+daemon/' {print} /etc/passwd` → Mostra as linha que começa por um caractere e após ela _“daemon”_.

`$ awk -F: ‘$3<100 {print $1,$3}' /etc/passwd` → Mostra as linhas as colunas 1 e 3 onde o UID (coluna 3) é menor que 100.

`$ awk -F: '$7 == "/bin/bash" {print $1,"usa", $7}' /etc/passwd` → Mostra os usuários (coluna 1) que utilizam o bash (/bin/bash, coluna 3) e insere a string _“usa”_ entre as duas colunas.

`$ awk -F: '$3 >= 100 && $3 <= 200 {print $1, $3}' /etc/passwd` → Mostra na tela os usuários (coluna 1) com UID (coluna 3) entre 100 e 200.

`$ awk -F: '/^b/ {print $1; count ++} END {print"Total:", count}' /etc/passwd` → Mostra as linhas que tem a primeira letra _“b”_ e faz um calculo utilizando `count` (um contador) mostrando no final o total.

`$ awk -F: '$3 >= 100 {print $1, $3; count ++} END {print"Total:", count}' /etc/passwd` → Mostra as colunas 1 e 3 somente das linhas em que a 3 coluna tem valor >= 100, faz um calculo utilizando `count` (um contador) mostrando no final o total

`$ awk -F: '{print toupper($1),$1}' /etc/passwd` → Mostra a primeira coluna transformada em maiúscula e em seguida a primeira coluna original.

`$ awk -F: '{print "\nUser:",$1,"\nUID:",$3}' /etc/passwd` → Mostra a primeira e a terceira coluna com formatação.

`$ awk -F: '{print "username: " $1, "\t\tuid:" $3}' /etc/passwd` → Mostra cada linha da 1 e 3 coluna com formatação com `\t` (tab).

`$ awk -F: '{count[$3]++} END {for (resource in count) print count[resource], resource}' /etc/passwd |sort -n` → Mostra cada linha juntamente com o número de vezes que a UID (coluna 3) se repete e ordena em ordem do menor pro maior (ou alfabetica) utilizando o `| sort -n` 

### Máterial Complementar:
https://www.hostgator.com.br/blog/como-usar-o-comando-awk-do-linux/

https://labex.io/tutorials/linux-linux-awk-command-text-processing-388493

---


## 4. `head`

### Para que serve?
Utilizado para **exibir as primeiras linhas de um arquivo**. 
**Por padrão são as primeiras 10 linhas.**

Pode ser aberto mais de um arquivo ao mesmo tempo.

### Opções:
- `-n N` → Escolhe a quantidade de linhas `N` para aparecer.
- `-v` → Inclui o cabeçalho.
- `-c N` → Seleciona os bytes `N`.
- `-q` → Tira o cabeçalho (mais de um arquivo).

### Sintaxe comum:
**`$ head [OPÇÕES] ARQUIVO`**

### Exemplos:
`$ head arquivo.txt` → Mostra as primeiras 10 linhas do arquivo

`$ head arquivo1.txt arquivo2.txt` → Mostra as primeiras 10 linhas de ambos os arquivos

`$ head -n 20 arquivo.txt` → Mostra as primeiras 20 linhas do arquivo.

`$ head -v arquivo.txt`  → Mostra o arquivo e o cabeçalho do arquivo.

`$ head -c 50 arquivo.txt` → Mostra os primeiros 50 bytes do arquivo.

`$ head -q arquivo1.txt arquivo2.txt` → Mostra as primeiras 10 linhas dos dois arquivos sem o titulo (separador) de cada arquivo.

### Máterial Complementar:
https://guialinux.uniriotec.br/head/

https://labex.io/tutorials/linux-linux-head-command-file-beginning-display-214302
---

## 5 `tail`

### Para que serve?
Utilizado para **exibir as últimas linhas de um arquivo**.
**Por padrão são as ultimas 10 linhas.**

Pode ser aberto mais de um arquivo ao mesmo tempo.

### Opções:
- `-c N` → Mostra os ultimos bytes `N` escolhidos.
- `-f` → Mostra um arquivo em crescimento (atualiza em tempo real).
- `-n N` → Mosta a quantidade `N` de linhas do final do arquivo.

### Sintaxe comum:
**`$ tail [OPÇÕES] ARQUIVO`**

### Exemplos:
`$ tail arquivo.txt` → Mostra as ultimas 10 linhas do arquivo.

`$ tail -n 20 arquivo.txt` → Mostra as ultimas 20 linhas do arquivo.

`$ tail -n +10 arquivo1.txt` → Mostra as ultimas linhas a partir da linha 10.

`$ tail -f /var/log/syslog` → Mostra o crescimento do arquivo `/var/log/syslog` em tempo real, pode ser qualquer arquivo que seja atualizado.

`$ tail -c 50 arquivo.txt` → mostra os últimos 50 bytes do arquivo.

### Máterial Complementar:
https://labex.io/tutorials/linux-linux-tail-command-file-end-display-214303

---

## 6. `less`

### Para que serve?
Utilizado para **visualizar arquivos de forma paginada e interativa**.
Pode ser utilizado após outros comandos, para mostrar o resultado do comando.

A interface do `man` funciona de forma semelhante.

### Opções:
Todos as opções só podem ser executados dentro do prórprio `less`, não há nenhuma que podem ser chamadas ou usadas ao usar o comando.

#### Dentro do less:
- `↓↑` → Rola uma linha para cima ou para baixo.
- `/termo` → Busca por "termo".
- `n` → Pula para a próxima ocorrência da busca.
- `b` → Volta uma página.
- `q` → Sai do less.

### Sintaxe comum:
**`$ less ARQUIVO`**

### Exemplos:
`$ less arquivo.txt` → Exibe o conteúdo do arquivo arquivo.

`$ less /var/log/syslog` → Exibe o conteúdo do arquivo de log `/var/log/syslog`.

`$ less +/termo arquivo.txt` → Abre o arquivo e já começa a busca pelo _"termo"_.

### Máterial Complementar:
Não possui material complementar.

---

## 7. `nl`

### Para que serve?
Utilizado para **numerar as linhas dos arquivos**.
No modo normal, numera somente as linhas com caracteres.

### Opções:
- `-b` → Mostra as linhas de acordo com o corpo do arquivo.
- `-b a` → Mostra todas as linhas numeradas, inclusive as em branco.
- `-b n` → Mostra todas as linhas sem número.
- `-b p` → Mostra somente as linhas numeradas, exceto aquelas com a equação.
- `-d` → Reinicia a contagem sempre que encontrar um delimitador.
- `-i N` - Incrementa em `N` o número da linha.
- `-l N` - Agrupa uma quantidade `N` de linhas como paragrafo.
- `-n` → Seleciona um formato especifico de numeração.
- `-n rz` → `-n` + alinha a numeração do lado esquerdo e adiciona zeros.
- `-s` → Escolhe um separador para as linhas e números (-s ,, -s ;, -s ‘->').
- `-v N` → Escolhe o número `N` para começar a contar.
- `-w` → escolhe o espaço entre os números e a lateral da página.

### Sintaxe comum:
**`$ nl [OPÇÕES] ARQUIVO`**

### Exemplos:
`$ nl arquivo.txt` → Mostra o arquivo com linhas numeradas (exceto as linhas em branco).

`$ nl -b a arquivo.txt` → Mostra o arquivo com todas as linhas numeradas.

`$ nl -b n arquivo.txt` → Mostra o arquivo com suas linhas não numeradas.

`$ nl -n rz arquivo.txt` → Mostra as linhas numeradas com zeros na lateral esquerda.

`$ nl -b p'^[^I]' arquivo.txt` → Mostra as linhas numeradas exceto aquelas que condizem com a equação.

`$ nl -s '->' arquivo.txt` → Modifica o separador entre os números e cada linha do arquivo.

`$ nl -w 30 arquivo.txt` → Escolhe o espaço entre a lateral e o número.

`$ nl -v 20 arquivo.txt` → Mostra as linhas numeradas e começa a contar a partir do 20 ao invés do 1.

`$ nl -i 3 arquivo.txt` → Mostra as linhas numeradas incrementando o número de cada uma em 3.

### Máterial Complementar:
Não possui material complementar.

---

## 8. `sort`

### Para que serve?
Utilizado para **organizar de forma rápida e simples as linhas**, sua forma padrão mantém em ordem alfabética.
Semelhante ao `Order by` em BD.

O comando não salva o arquivo organizado por padrão, apenas exibe na tela.

### Opções:
- `-b` → Ignora espaços em branco.
- `-c` → Retorna uma mensagem de erro se o arquivo não estiver ordenado.
- `-f` → Ignora a diferença entre letras maiúsculas e letras minúsculas.
- `-k` → Escolhe qual coluna vai ser utilizada o sort (utilizado com o -t).
- `-M` → Organiza por ordem de mês, desde que os meses estejam na mesma lingua do sistema.
- `-n` → Organiza por ordem numérica.
- `-r` → Reverte a ordem do sort.
- `-t` → Especifica o separador de colunas.
- `-u` → Retira os clones.

Caso o números sejam filtrados sem o `-n`, vão ser contados como caracteres e não como números, como por exemplo: 18, 19, 20, 21, 3, 45.

### Sintaxe comum:
**`$ sort [OPÇÕES] ARQUIVO`**

### Exemplos:
`$ sort arquivo.txt` → Organiza a ordem das linhas do arquivo em ordem alfabética.

`$ sort -n -t: -k2 arquivo.txt` → Organiza o arquivo em ordem numérica, com base na segunda coluna separada por _“:”_.

`$ sort -nr -t ':' -k2 arquivo.txt` → Organiza o arquivo em ordem numérica reversa, com base na segunda coluna separada por _“:”_.

`$ sort -t: -k2n -k3nr arquivo.txt` → Organiza o arquivo em ordem numérica com base na segunda coluna e em ordem numérica reversa com base na terceira coluna, como retorno pode ter:  _“A:18:92”_, _“E:18:91”_ e _“C:19:95”_.

`$ sort -u arquivo.txt` → Organiza o arquivo em ordem alfabética retirando os clones.

`$ sort -u -fb nomes.txt` → Organiza o arquivo em ordem alfabética retirando os clones, desconsiderando espaços e a diferença entre letras maiúsculas e minusculas.

`$ sort arquivo.txt > arquivoorganizado.txt`  → Organiza o arquivo em ordem alfabética e salva ele em outro arquivo.

### Máterial Complementar:
https://labex.io/tutorials/linux-linux-sort-command-text-sorting-219196

https://guialinux.uniriotec.br/sort/

---

## 8. `tac`

### Para que serve?
Utilizado para **exibir o conteúdo de um arquivo de trás para frente**, ou seja, ele imprime as linhas de um arquivo em **ordem reversa**.

É essencialmente o oposto do comando `cat` quando falamos de imprimir dados na tela, mas vale lembrar que o comando `cat` faz muito mais.

### Opções:
- `-b` → Adiciona coloca o separador antes de cada linha, em vez de colocar depois.
- `-s` → Especifica um delimitador, ao invé de nova linha.

### Sintaxe comum:
**`$ tac [OPÇÕES] ARQUIVO`**

### Exemplos:
`$ tac arquivo.txt` → Mostra o arquivo em ordem decrescente de linhas.

`$ tac -b arquivo.txt` → Mostra o arquivo tirando 

### Máterial Complementar:
Não possui material complementar.

---

## 10. `uniq`

### Para que serve?
Utilizado para **filtrar e contar as linhas repetidas de um arquivo**.

O `uniq` só remove duplicatas adjacentes, ou seja, as **linhas repetidas que estão em sequência**.

### Opções:
- `-c` → Exibe a quantidade de cada linha duplicada.
- `-d` → Exibe somente as linhas duplicadas (ocorrem mais de uma vez).
- `-f N` → Pula os primeiros `N` campos da linha comparada.
- `-i` → Ignora diferenças entre maiúsculas e minúsculas.
- `-s N` → Pula os primeiros `N` caracteres da linha comparada.
- `-u` → Exibe somente as linhas únicas (não duplicadas).

### Sintaxe comum:
**`$ uniq [OPÇÕES] ARQUIVO`**

### Exemplos:
`$ uniq arquivo.txt` → Remove linhas duplicadas no arquivo.

`$ uniq arquivo.txt arq_uniq.txt` → Remove linhas duplicadas adjacentes do arquivo e insere em um novo arquivo.

`$ uniq -c arquivo.txt` → Exibe as linhas com contagem de quantas vezes cada uma aparece.

`$ uniq -d arquivo.txt `→ Mostra apenas as linhas duplicadas.

`$ uniq -u arquivo.txt` → Mostra apenas as linhas que não se repetem.

`$ uniq -i arquivo.txt` → Remove duplicatas, ignorando diferenças de maiúsculas e minúsculas.

### Máterial Complementar:
Não possui material complementar.
