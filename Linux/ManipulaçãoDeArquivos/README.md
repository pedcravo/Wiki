# Comandos para Manipulação de Arquivos

Nesta seção, exploramos comandos que permitem manipular arquivos e diretórios no Linux. Esses comandos são essenciais para copiar, mover, alterar permissões, criar e remover arquivos e diretórios.

### Comandos:

1. [`chgrp`](#1-chgrp)
2. [`chmod`](#2-chmod)
3. [`chown`](#3-chown)
4. [`cp`](#4-cp)
5. [`expand`](#5-expand)
6. [`unexpand`](#6-unexpand)
7. [`ln`](#7-ln)
8. [`mkdir`](#8-mkdir)
9. [`mv`](#9-mv)
10. [`paste`](#10-paste)
11. [`rm`](#11-rm)
12. [`rmdir`](#12-rmdir)
13. [`split`](#13-split)
14. [`touch`](#14-touch)

---

## 1. `chgrp`

### Para que serve?
O comando `chgrp` (Change Group) é usado para **modificar a propriedade do grupo associado a um arquivo**, permitindo que grupos diferentes tenham controle de leitura, escrita ou execução sobre o arquivo.

Esse comando é especialmente útil em ambientes multi usuário, onde diferentes grupos de trabalho precisam gerenciar arquivos em conjunto.

#### Arquivos Relacionados:
- `/etc/group`: Contém informações sobre grupos de usuários no sistema.

### Opções:
- `-c` → Exibe as alterações feitas. Similar ao `-v`, mas mostra apenas quando uma alteração de grupo ocorre.
- `-f` → Suprime a maioria das mensagens de erro. Se houver falhas no comando, elas não serão exibidas no terminal.
- `-h` → Afeta links simbólicos em vez dos arquivos apontados por eles. Usado em sistemas que permitem alterar a propriedade de links simbólicos.
- `-R` → Aplica a mudança de grupo a todos os arquivos e subdiretórios dentro de um diretório.
- `--reference=RFILE` → Altera o grupo de um arquivo ou diretório com base nas permissões de grupo do `RFILE` especificado.
- `-v` → Mostra um diagnóstico para cada arquivo processado, independentemente de ter sido alterado ou não.

### Sintaxe comum:
**`$ chgrp [OPÇÕES] GRUPO ARQUIVO`**

### Exemplos:
`# chgrp backend file.txt` → Altera o grupo proprietário do arquivo para o grupo `backend`.

`# chgrp -R staff /office/files` → Altera recursivamente o grupo de todos os arquivos e diretórios dentro de `/office/files`.

`# chgrp --reference=arquivo.exe file.txt` → Altera o grupo do arquivo `file.txt` para o mesmo grupo de `arquivo.exe`.

`# chgrp -h backend link_sim` → Altera o grupo dono do link simbólico sem alterar o arquivo base (o arquivo na qual ele aponta).

### Máterial Complementar:
<img src="https://github.com/pedcravo/Wiki/blob/main/Linux/ChgrpChmodChown.png" width="600px">

<img src="https://github.com/pedcravo/Wiki/blob/main/Linux/PermissoesQuadro.png" width="600px">

https://www.linuxforce.com.br/comandos-linux/comandos-linux-comando-chgrp/

---

## 2. `chmod`

### Para que serve?
Utilizado para **alterar as permissões de usuários** sobre arquivos e diretórios.

**Somente o usuário root e o owner podem alterar as permissões**

### Sistema de Permissões:
`----------` ↔ `-|---|---|---|` ↔ `-|u|g|o|`

#### Classificação do Arquivo: (-)--- --- ---
- `-` → **tipo** → Indica se é arquivo (-) ou diretório (d) ou link (l).

#### Grupos de Permissões: -(---)(---)(---)
- `u` → **user** → Dono/criador do arquivo.
- `g` → **group** → Usuários do grupo dono.
- `o` → **others** → Outros usuários.
- `a` → **all** → Todos.

#### Permissões em cada Grupo:
- `r` → **read** → Permissão para ver o que tem no arquivo.
- `w` → **write** → Permissão para modificar o arquivo.
- `x` → **execute** → Permissão para executar/rodar o programa (script).

#### Utiliza o sistema octal para conceder permissões
Binário | Octal
:----:|:----:
000 | 0
001 | 1
010 | 2
011 | 3
100 | 4
101 | 5
110 | 6
111 | 7

### Opções:
- `U+P` → Qualquer usuário `+` permissão.
- `U-P` → Qualquer usuário `-` permissão.
- `ugo` → Número das permissões de cada usuário na ordem.

#### Permissões comuns:
- `644` - File Baseline.
- `755` - Directory Baseline.
- `400` - Key Pair.

### Sintaxe comum:
**`$ chmod PERMISSÃO ARQUIVO`**

### Exemplos:
`$ chmod u+r arquivo.png` → Dá permissão de `read` ao `owner`, as permissões se tornarão → `-r--rw-r-x`.

`$ chmod g-r arquivo.png` → Tira a permissão de `read` ao `group`, as permissões se tornarão → `-r---w-r-x`.

`$ chmod g+rx arquivo.png` → Dá permissão de `read` e `execute` ao `group`, as permissões se tornarão → `-r--rwxr-x`.

`$ chmod a-r arquivo.png` → Dá permissão de `read` ao `owner`, as permissões se tornarão → `-----wx--x`.

### Máterial Complementar:
<img src="https://github.com/pedcravo/Wiki/blob/main/Linux/ChgrpChmodChown.png" width="600px">

<img src="https://github.com/pedcravo/Wiki/blob/main/Linux/PermissoesQuadro.png" width="600px">

https://labex.io/tutorials/linux-logical-commands-and-redirection-387332

https://www.youtube.com/watch?v=LnKoncbQBsM

---

## 3. `chown`

### Para que serve?
Utilizado para **gerenciar permissões, alterar o proprietário e/ou grupo** de um arquivo ou diretório.
O chown também pode ser usado para **alterar as permissões de diretórios de maneira recursiva**, alterando o proprietário de todos os arquivos e subdiretórios.

É possível checar alterações no arquivo com `ls -l`.

**Comando funciona melhor com sudo.**

### Opções:
- `-h` → Usado para mudar o dono do link simbólico.
- `-R` → Utilizado para fazer a mudança de dono dos arquivos de forma recursiva.
- `-v` → Modo verboso, exibe uma mensagem para cada arquivo que é modificado.

### Sintaxe comum:
#### Em arquivos
**`$ chown [OPÇÕES] USUARIO :GRUPO ARQUIVO`**

#### Em diretórios
**`$ chown [OPÇÕES] USUARIO :GRUPO /DIRETORIO`**

#### Em Links Simbólicos
**`$ chown [OPÇÕES] USUARIO :GRUPO LINK`**

### Exemplos:
#### Em Arquivos
`$ chown pedro arquivo.txt` → Muda o dono do arquivo para `pedro`.

`$ chown pedro:backend arquivo.txt` → Muda o dono do arquivo para `pedro` e o grupo do arquivo para `backend`.

`$ chown :backend arquivo.txt` → Muda o grupo do arquivo para `backend`.

`$ chown --reference=arquivo1 arquivo2` → Altera o dono e o grupo do `arquivo2` para os mesmos do `arquivo1`.

#### Em Diretórios
`$ chown root /dir` → Muda o dono do diretório para `root`.

`$ chown root:backend /dir` → Muda o dono do diretório para `root` e o grupo do diretório para `backend`.

`$ chown :backend /dir` → Muda o grupo do diretório para `backend`.

`$ chown -R pedro:backend ~/Downloads` → Altera o dono e o grupo do diretório `Downloads` e de todos os arquivos dentro dele de forma recursiva.

#### Em Links Simbólicos
`$ chown pedro link_arquivo` → Altera o dono do arquivo base do link.

`$ chown -h pedro link_arquivo` → Altera o dono do link simbólico.

### Máterial Complementar:
<img src="https://github.com/pedcravo/Wiki/blob/main/Linux/ChgrpChmodChown.png" width="600px">

<img src="https://github.com/pedcravo/Wiki/blob/main/Linux/PermissoesQuadro.png" width="600px">

https://labex.io/tutorials/linux-logical-commands-and-redirection-387332

https://www.youtube.com/watch?v=LnKoncbQBsM

---

## 4. `cp`

### Para que serve?
Utilizado para **copiar arquivos ou diretórios** de um diretório para outro.

### Opções:
- `-i` → Faz checagem de segurança, se há um arquivo com este nome.
- `-l` → Cria links.
- `-n` → Não sobrescreve um arquivo existente.
- `-p` → Preserva os dados do arquivo original na cópia, como: data da modificação, tempo de acesso e permissão.
- `-r` → Pesquisa recursivamente nos diretórios.
- `-s` → Cria links simbólicos em vez de copiar arquivos (atualiza junto com o original).
- `-u` → Copia apenas quando o arquivo de origem é mais novo do que o arquivo de destino ou quando o arquivo de destino está faltando.
- `-v` → Mostra com mais detalhes o processo que está acontecendo.

### Sintaxe comum:
**`$ cp [OPÇÕES] ARQUIVO.. CÓPIA_ARQUIVO`**

### Exemplos:
$ cp exemploarquivo arquivoexemplo → copia o exemploarquivo trocando o nome para arquivoexemplo no mesmo diretório.

$ cp arquivo1.txt arquivo2.txt arquivo3.txt arquivo4.txt ~/Downloads/copias_arquivos → copia vários arquivos para dentro de um aquivo.

$ cp exemploarquivo /home/pedrocravo/Downloads/ → copia o exemploarquivo do local para o diretório Downloads.

$ cp /home/pedrocravo/Downloads/exemploarquivo arquivoexemplo → copia o arquivo do diretório Downloads para o local, dando a ele o nome arquivoexemplo.

$ cp ~/Documentos/[a-e]* ~/Downloads → copia arquivos ou diretórios do diretório Documentos que o nome começa com qualquer letra de "a" até "e", para o diretório Downloads.

$ cp ~/Documentos/[a]* exemplopasta → copia arquivos ou diretórios do diretório Documentos que o nome começa com "a", para o diretório exemplopasta (que está dentro do diretório Documentos).

$ cp -r diretorio1 diretorio2 → copia diretório com arquivos com recursão e da a cópia um novo nome.
$ cp -r diretorio /home/pedrocravo → copia diretório com arquivos para outro lugar.

### Máterial Complementar:

---

## 5. `ln`

### Para que serve?

### Opções:

### Sintaxe comum:

### Exemplos:

### Máterial Complementar:

---

## 6. `mkdir`

### Para que serve?

### Opções:

### Sintaxe comum:

### Exemplos:

### Máterial Complementar:

---

## 7. `mv`

### Para que serve?

### Opções:

### Sintaxe comum:

### Exemplos:

### Máterial Complementar:

---

## 8. `paste`

### Para que serve?

### Opções:

### Sintaxe comum:

### Exemplos:

### Máterial Complementar:

---

## 9. `rm`

### Para que serve?

### Opções:

### Sintaxe comum:

### Exemplos:

### Máterial Complementar:

---

## 10. `rmdir`

### Para que serve?

### Opções:

### Sintaxe comum:

### Exemplos:

### Máterial Complementar:

---

## 11. `touch`

### Para que serve?

### Opções:

### Sintaxe comum:

### Exemplos:

### Máterial Complementar:
