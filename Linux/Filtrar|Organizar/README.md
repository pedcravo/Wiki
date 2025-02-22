# Comandos para Filtrar e Organizar Dados
Nesta seção, exploramos comandos que permitem filtrar e organizar dados no Linux.
Estes comandos são amplamente utilizados para **manipulação de texto e processamento de arquivos, permitindo operações como filtrar e recortar dados de forma flexível**.

### Comandos:

1. [`cat`](#cat)
2. [`tac`](#tac)
3. [`cut`](#cut)
4. [`grep`](#grep)
5. [`awk`](#awk)
6. [`echo`](#echo)
7. [`head`](#head)
8. [`tail`](#tail)
9. [`less`](#less)
10. [`nl`](#nl)
11. [`sort`](#sort)
12. [`tr`](#tr)
13. [`uniq`](#uniq)
14. [`wc`](#wc)

## `cat`

### Para que serve?
O comando `cat` é utilizado para **juntar (concatenar) arquivos**. Em sua forma base, ele também pode ser utilizado para **visualizar o conteúdo de arquivos** diretamente no terminal.

### Opções:
- `-n` → Mostra os números de cada linha do arquivo.
- `-v` → Mostra caracteres não imprimíveis, como acentos ou quebras de linha.

### Sintaxe comum:
**`$ cat [OPÇÕES] ARQUIVO`**

### Exemplos:
`$ cat arquivo.txt` → Mostra o arquivo `.txt` na tela.

`$ cat arquivo.txt - arquivo1.txt` → Mostra o arquivo .txt na tela e redireciona o conteúdo para outro arquivo `.txt`.

`$ cat arquivo1.txt arquivo2.txt > arquivo_combinado.txt` → Mostra os arquivos .txt na tela na tela e concatena ambos em um arquivo novo `.txt`.

`$ cat > arquivo_novo.txt` → Cria um novo arquivo e permite inserir dados manualmente (uma linha).

`$ cat >> arquivo.txt` → Atualiza o arquivo `.txt` ao invés de sobrescrevê-lo.

`$ cat -n arquivo1.txt` → Mostra a numeração de cada linha.

`$ cat -v arquivo2.txt` → Mostra caracteres não imprimíveis.

### Máterial Complementar:
https://ryanstutorials.net/linuxtutorial/vi.php

---

## `tac`

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

## `cut`

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

## `grep`

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
- `-ic` ↔ `-i` + `-c`
- `-vi` ↔ `-v` + `-i`
- `-ri` ↔ `-r` + `-i`
- `-rli` ↔ `-r` + `-l` + `-i`

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

`$ egrep -w '[[:lower:]]{5}' grep-file.txt` → Procura pelas palavras com apenas 5 letras minusculas.

`$ egrep '[[:lower:]]{5}' grep-file.txt` → Procura pelas palavras com 5 letras minusculas.

`$ egrep -w '[[:alpha:]]{5}' grep-file.txt` → Procura pelas palavras com apenas 5 letras, minusculas ou maiusculas.

`$ egrep -w '[[:upper:]]{5,}' grep-file.txt` → Procura pelas palavras com 5 ou mais letras maiusculas.

`$ egrep '.{40,}' grep-file.txt` → Procura pelas linhas com 40 ou mais letras.

`$ egrep 'f(a|o)r' grep-file.txt` → Filtra somente as palavras que comecem com a letra _f_, _a_ ou _o_ e por fim _r_.

`$ egrep 'f[ao]r' grep-file.txt` → Filtra somente as palavras que comecem com a letra _f_, _a_ ou _o_ e por fim _r_.

#### fgrep
`$ fgrep "?" arquivo.txt` → Procura as linhas que tenham o caractere `?` ( tem como equivalente `grep`: `$ grep "\?" arquivo.txt`).

### Máterial Complementar:
https://www.hostinger.com.br/tutoriais/comando-grep-linux

https://labex.io/tutorials/linux-linux-grep-command-pattern-searching-219192

https://cloudminister.com/blog/how-to-use-grep-command-in-linux/

https://ryanstutorials.net/linuxtutorial/grep.php

https://github.com/BurntSushi/ripgrep

---

## `awk`

### Para que serve?
Utilizado para **filtra, recortar, printar** e etc.

É semelhante ao `cut` + `grep`.

**É possível utilizar [Meta Caracteres](../MetaCaractere/README.md), funções Lambda, funções com string e etc**.

### Opções:
- `-F` → Tem como padrão para pesquisa o separador: _“:”_ mas pode ser alterado por _“,”_, _“.”_ dentre outros.

#### Tipos de seletores de caracteres:
- `$N` → Escolhe a coluna `N`.
- `$N,$M` → Escolhe as colunas `N` e `M`, $0 corresponde a linha inteira linha inteira.
- `”palavra”` → Usado quando inserir string
- `BEGIN` → Usado para fazer uma ação ao começar a rodar.
- `END` → Usado para fazer uma ação depois que a anterior terminar (final).
- `FS` → Usado para especificar o separador de campo (linha) para filtragem.
- `RS` → Usado para especificar o separador de registro (coluna) para filtragem.
- `OFS` → Usado para especificar o separador de coluna ao mostrar.
- `FNR` → Variável usada para contar as linhas de um arquivo (reinicia a cada novo arquivo), armazena o número de cada linha.
- `NR` → Variável usada para contar as linhas de vários arquivos (continua contando a cada novo arquivo), armazena o número total de linhas.

### Sintaxe comum:
**`$ awk [OPÇÕES] 'CARACTERE {print $NUMERO-DA-COLUNA}' ARQUIVO`**

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

`$ awk 'NR==3, NR==6 {print NR,$0}' employee.txt` → Mostra apenas as linhas de 3 a 6 numeradas.

`$ history | awk '{a[$2]++}END{for(i in a){print a[i] " " i}}' | sort -rn | head` → Conta cada comando, em seguida mostra os comandos mais utilizados e quantas vezes aqueles comando foi utilizado.

`# dmidecode | awk '/Product Name/,/Manufacturer/'` → Mostra qual o nome do produto e quem o fez, por quem foi produzido.

`# awk '!x[$0]++' arquivo.txt` → Filtra as linhas repetidas, não altera o arquivo original.

`$ tail -100 arquivo.txt | awk '{print $1}' | sort | uniq -c | sort -n | tail` → Conta cada linha que tem a 1ª coluna reptida e organiza do menos repetido para o mais repetido, em seguida mostra o total de repetição daquel coluna e cada coluna.

`# last  | grep -v "^$" | awk '{print $1}' | sort -nr | uniq -c` → Mostra os usuários que mais acessaram o sistema por nome.

`# netstat -ntu | awk '{print $5}' | cut -d: -f1,2 | sort | uniq -c | sort -n` → Mostra os endereços acessados e a quantidade de vezes acessada.

`# netstat -ant | awk '{print $NF,$3,$4,$5}' | grep -v '[a-z]' | sort | uniq -c` → Mostra as conexões estabelecidas e em escuta organizadas em ordem alfabética.

`# du -d 1 | sort -r -n | awk '{split("KB(s) MB(s) GB(s)",v); s=1; while($1>1024){$1/=1024; s++} print int($1)" "v[s]"t"$2}'` → Mostra os diretórios organizados por tamanho.

`$ awk 'BEGIN{FS="\n"; RS=""}{print $1,$3}' arquivo.txt` → Organiza a 1ª e 3ª linha e as mostr na tela na mesma linha.

`$ awk 'BEGIN{FS="\n"; RS=""; OFS="\n"}{print $1,$3}' arquivo.txt` → Organiza a 1ª e 3ª linha e as mostr na tela uma sobre a outra.

`$ awk 'BEGIN{FS="\n"}{print $1, "FNR="FNR}' arquivo.txt` → Mostra todas as linhas do arquivo mostrando o valor de FNR em cada linha, o FNR equivale ao número da linha.

`$ awk 'BEGIN{FS="\n"}{print $1, "FNR="FNR, "NR="NR}END{print "Total de linhas: "NR}' arquivo.txt arquivo.txt` → Mostra todas as linhas do arquivo mostrando o valor de FNR e NR em cada linha, por fim mostra o NR total.

``` bash
$ awk '
BEGIN{
str1="Bem vindo"
str2=", olá"
str3=str1 str2
print str3
}'
```
Cria 3 variáveis string `str1`, `str2` e `str3`, mostrando na tela a `str3`. 

`$ awk '{if ($1 < 50) print $1}' arquivo.txt}` → Mostra somente as linhas que a primeira coluna tem um valor menor que 50.

```bash
$ awk '{
if ($1 >50){
varx= $1 *2
print varx}
else{
varx= $1 *3
print varx }}' texto.txt 
```
Mostra os números do arquivo de maneira que se o valor for > 50 ele é multiplicado por dois e mostrado na tela, caso não seja ele é multiplicado por 3 e mostrado na tela. Pode ser reescrito desta maneira: `$ awk '{if ($1 > 50) print $1 *2; else print $1 *3}' texto.txt`

```bash 
$ awk '{
total = 0
i = 1
while (i < 4)
{
total += $i
i++
}
media = total/3
print "Valor médio: ", media
}' texto.txt 
```
Mostra a média de cada linha. Pode ser reescrito com o loop for.
```bash 
$ awk '{
total = 0
for (i=1; i < 4; i++)
{
total += $i
}
media = total/3
print "Valor médio: ", media
}' texto.txt 
```

### Máterial Complementar:
https://www.hostgator.com.br/blog/como-usar-o-comando-awk-do-linux/

https://labex.io/tutorials/linux-linux-awk-command-text-processing-388493

---

## `echo`

### Para que serve?
O comando `echo` é usado para **imprimir uma string, texto ou o valor de uma variável no terminal**, sendo uma ferramenta básica para criar saídas de texto em scripts e interações no shell.

### Opções:
- `-e` → Habilita interpretação dos códigos de escape após barra invertida.
- `-E` → Desabilita a interpretação dos códigos de escape (comportamento padrão em algumas distribuições).
- `-n` → Não adiciona uma nova linha após mostrar os argumentos.

#### Códigos de escape:
- `\\` → Exibe uma barra invertida.
- `\a` → Alerta (Sino).
- `\b` → Retroceder.
- `\c` → Não permite saída após esta.
- `\e` → Caractere de escape.
- `\f` → Alimentação de página (FF).
- `\n` → Nova linha (NL).
- `\r` → Retorno de carro (CR).
- `\t` → Tabulação horizontal.
- `\v` → Tabulação vertical.
- `\ 0 NNN` → Byte com valor octal `NNN` (que pode ter de 1 a 3 dígitos).
- `\ x HH` → Byte com valor hexadecimal `HH` (que pode ter 1 ou 2 dígitos).

### Sintaxe comum:
**`$ echo [OPÇÕES] ARQUIVO *ESCAPE*`**

### Exemplos:
`$ echo /*` → Mostra todo o conteúdo do diretório raiz em ordem alfabética.

`$ echo “Eu tenho $[2024 - 2005] anos de idade.”` → Mostra na tela a mensagem acima e faz o calculo.

`$ echo “Há $(ls | wc -w) arquivos nesse diretório.”` → Mostra a mensagem na tela e também a soma de arquivos no diretório.

`$ echo -e 'Hello World\nOlá Mundo'` → Mostra a mensagem entre aspas simples utilizando o `\n` para pular uma linha entre uma palavra e outra.

`$ echo -e 'Hello World\a'` → Mostra a mensagem entre aspas simples utilizando o `\a` para tocar um som.

`$ echo -E 'É só escrever \n para pular linha'` → Mostra a mensagem entre aspas simples interpretando o `\n` como uma mensagem e não como um código.

`$ echo "Conteúdo do arquivo" > arquivo.txt` → Substitui o conteúdo do arquivo pela mensagem ou cria o arquivo com a mesagem.

`$ ls -la | grep arquivo ; echo -e '\n' ~/Downloads/* '\a'` → Executa uma série de comandos, `ls` procurando todos os arquivos e em seguida é utilizado o `grep` sobre a saída do comando anterior para filtrar os arquivos, em seguida é executado o comando `echo` que pula uma linha, mostra os arquivos dentro de `Downloads` e seus caminhos e depois toca um sino.

### Máterial Complementar:
https://guialinux.uniriotec.br/echo/

---

## `head`

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

## `tail`

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

`$ tail -c 50 arquivo.txt` → mostra os últimos 50 bytes do arquivo.

`$ tail -f /var/log/syslog` → Mostra o crescimento do arquivo `/var/log/syslog` em tempo real, pode ser qualquer arquivo que seja atualizado.

`$ tail /var/log/auth.log` → Mostra os logs de auth, que registram todos os eventos e atividades relacionadas à autenticação que ocorreram no servidor. Isso inclui, entre outros, logins do sistema, alterações de senha e comandos emitidos sudo.

### Máterial Complementar:
https://labex.io/tutorials/linux-linux-tail-command-file-end-display-214303

---

## `less`

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

`$ less /etc/group` → Mostra todos os grupos no linux.

### Máterial Complementar:
Não possui material complementar.

---

## `nl`

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

## `sort`

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

## `tr`

### Para que serve?
O comando `tr` é utilizado para **substituir, remover ou compactar caracteres** em um fluxo de texto. O comando `tr` lê da **entrada padrão** (texto e arquivo) e escreve na saída padrão após aplicar as transformações especificadas.

### Opções:
- `-c` → Complementa o conjunto de caracteres, selecionando tudo o que não está no conjunto especificado.
- `-d` → Deleta/remover os caracteres especificados da entrada.
- `-s` → Suprime (remove duplicatas) consecutivas de caracteres especificados, deixando apenas uma ocorrência.
- `-t` → Trunca o comprimento de `SET2` para que ele corresponda exatamente ao comprimento de `SET1`.

#### Conjuntos de caracteres:
- `[:punct:]` → Se refere a toda pontuação.
- `[:digit:]` → Se refere a somente os dígitos.

### Sintaxe comum:
**`$ tr [OPTION]... SET1 [SET2]`**
`SET1` → Especifica os caracteres que serão transformados.
`SET2` → Especifica para quais caracteres serão substituídos.

### Exemplos:
`$ cat arquivo.txt | tr 'a-z,ç,ã' 'A-Z,Ç,Ã'` → Transforma todas as letras minúsculas dentro do arquivo em letras maiúsculas.

`$ echo "hello world" | tr ' ' '_'` → Substitui espaços por underscores.

`$ echo "olá pedro" | tr -d 'o'` → Remove todas as letras “`o`" do comando echo.

`$ cat arquivo.txt | tr -d '[:punct:]’` → Retira toda a pontuação do arquivo.

`$ cat tr.nano.txt | tr 'b-za-a' 'a-z’` → Troca as letras do arquivo por uma letra antes (b → a, c → b, e assim por diante).

`$ echo "abcdef" | tr -t 'abc' 'XYZUV'` → Truncará o SET2 para 'XYZ', correspondendo ao tamanho de 'abc'.

`$ cat ~/project/log_entry.txt | tr -cd '[:digit:]’` → Remove os dígitos do arquivo, deixando somente os números sobrarem.

`$ cat ~/project/spaced.txt | tr -s ' ‘` → Retira os espaços repetidos.

### Máterial Complementar:
https://labex.io/tutorials/linux-linux-tr-command-character-translating-388064

---

## `uniq`

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

---

## wc

### Para que serve?
Utilizado para **mostrar linhas, palavras e números de caracteres** em um ou mais arquivos.

### Opções:
- `-c` → Conta o número de Bytes.
- `-l` → Conta o número de linhas.
- `-L` → Conta o comprimento da linha mais longa.
- `-m` → Conta o total de caracteres.
- `-w` → Conta as palavras de um ou mais arquivos.

### Sintaxe comum:
**`$ wc [OPÇÕES] ARQUIVO`**

### Exemplos:
`$ wc arquivo.txt` → Exibe o número de linhas, palavras e bytes do arquivo.

`$ wc -l arquivo.txt` → Exibe apenas o número de linhas no arquivo.

`$ wc -w arquivo.txt` → Exibe apenas o número de palavras  no arquivo.

`$ wc -m arquivo.txt` → Exibe apenas o número de caracteres  no arquivo.

`$ wc -c arquivo.txt` → Exibe o número de bytes  no arquivo.

`$ wc -l -w -m arquivo.txt` → Exibe o número de linhas, palavras e caracteres do arquivo.

### Máterial Complementar:
https://labex.io/tutorials/linux-linux-nl-command-line-numbering-210988
