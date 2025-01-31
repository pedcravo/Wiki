# Comandos para navegar pelo sistema

Nesta sessão iremos ver sobre os comandos utilizados para navegar pelo sistema.

### Comandos:

1. [`cd`](#cd)
2. [`dir`](#dir)
3. [`ls`](#ls)
4. [`pwd`](#pwd)
5. [`tree`](#tree)

## `cd`

### Para que serve?
Utilizado para **navegar entre diretórios**.
(Change Directory)

### Refenciamento:
- `.` → Diretório atual.
- `..` → Diretório acima.
- `../../` → Um diretório acima do diretório acima.
- `~/` ,`~` ou ` ` → Diretório padrão do usuário.
- `/` → Diretório `root`.

### Sintaxe comum:
**`$ cd DIRETÓRIO`**

### Exemplos:
`$ cd` → Vai para o /home.
`$ cd ..` → Vai para um diretório acima.
`$ cd Documentos` → Vai para o diretório *Documentos* a partir do `/home/pedrocravo`.
`$ cd /home/pedrocravo/Documentos` → vai para o diretório Documentos.
`$ cd ~/Documentos` → Vai para o diretório Documentos.
`$ cd /` → Vai para o diretório raiz, root.

### Máterial Complementar:
https://guialinux.uniriotec.br/cd/

---

## `dir`

### Para que serve?
Utilizado para **listar o conteúdo de uma diretório**.
(Directory)

### Opções:
- `-a` → Mostra arquivos ocultos.

### Refenciamento:
- `.` → Diretório atual.
- `..` → Diretório acima.
- `../../` → Um diretório acima do diretório acima.
- `~/` ,`~` ou ` ` → Diretório padrão do usuário.
- `/` → Diretório `root`.

### Sintaxe comum:
**`$ dir DIRETÓRIO`**

### Exemplos:
`$ dir` → Mostra o conteúdo do diretório atual.

`$ dir -a` → Lista o conteúdo de um diretório juntamente com os arquivos ocultos.

### Máterial Complementar:
https://sobrelinux.info/questions/7004/difference-between-dir-and-ls-terminal-commands

---

## `ls`

### Para que serve?
Utilizado para **listar arquivos ou diretórios e mostrar suas propriedades**.
(LiSt directory contents)

### Opções:
- `-a` → Mostra todos os arquivos (normais + ocultos).
- `-A` → Mostra todos os arquivos (normais + ocultos) exeto `.` e `..`.
- `-d` → Mostra apenas diretórios.
- `-h` → Mosta tamanhos de arquivo com notações KB e MB.
- `-l` → Mostra propriedades (permissões) dos arquivos em forma de coluna.
- `-r` → Reverte a organização (decrescente).
- `-R`  → Mostra o diretório atual e seus subdiretórios até o ultimo arquivo (recursividade).
- `-s` → Mostra arquivos e seus tamanhos.
- `-S` → Ordena por tamanho decrescente.
- `-t` → Ordena por ultima data e hora de modificação em ordem decrescente.
- `*` → Mostra diretórios e seus subdiretórios.
- `>` → Transforma a saida em um arquivo.

### Refenciamento:
- `.` → Diretório atual.
- `..` → Diretório acima.
- `../../` → Um diretório acima do diretório acima.
- `~/` ,`~` ou ` ` → Diretório padrão do usuário.
- `/` → Diretório `root`.

### Sintaxe comum:
**`$ ls [OPÇÕES] DIRETÓRIO`**

### Exemplos:
`$ ls` → Mostra arquivos normais no local.

`$ ls ..` → Mostra arquivos em um diretório acima.

`$ ls -d` → Mostra o diretório atual.

`$ ls -d */` → Mostra todos os diretórios dentro do diretório atual.

`$ ls -ld` → Mostra as as propriedades do diretório atual.

`$ ls Documentos`  → Mostra arquivos dentro do diretório Documentos a partir do `/home/pedrocravo`.

`$ ls ~/Documentos` → Mostra os arquivos dentro do diretório Documentos.

`$ ls /bin` → Mostra todos os comandos já executados no shell desta máquina.

`$ ls > saida.txt` → Transforma a pesquisa em um arquivo `.txt`.

`$ ll` → É um aliás para `ls -alF`.

### Máterial Complementar:
<img src="https://github.com/pedcravo/Wiki/blob/main/Linux/$ls.png" width="600px">

https://www.freecodecamp.org/portuguese/news/o-comando-ls-do-linux-como-listar-arquivos-em-um-diretorio-e-flags-de-opcao/

<img src="https://github.com/pedcravo/Wiki/blob/main/Linux/ls_-l.webp" width="600px">

---

## `pwd`

### Para que serve?
Utilizado para **mostrar o caminho do diretório atual**.
(Print Working Directory)

### Exemplos:
`$ pwd`

### Máterial Complementar:
https://pt.linkedin.com/pulse/comandos-de-navega%C3%A7%C3%A3o-comando-ls-e-cd-idal%C3%A9cio-silva

---

## `tree`

### Para que serve?
O comando `tree` do Linux **lista o conteúdo dos diretórios em formato de árvore**, podendo ser usado para a estrutura do sistema de arquivos. A estrutura exibida depende dos parâmetros especificados no prompt de comando.

Para instalar o `tree`: `sudo apt install tree`

### Opções:
- `-a` → Lista todos os arquivos, inclusive os ocultos.
- `-d` → Lista somente os subdiretórios.
- `-D` → Mostra a data da ultima atualização.
- `-f` → Exibe o caminho completo dos arquivos.
- `-p` → Exibe as permissões dos arquivos.
- `-s` → Mostra o tamanho de cada arquivo junto com o nome.
- `−−help` → Exibe as opções do utilitário.
- `−−version` → Mostra informações sobre o utilitário .

### Sintaxe comum:
**`tree [OPÇÃO]`**

### Exemplos:
`$ tree -I 'exemplo * | bin | lib'` → Mostra uma `tree` que comece com “`exemplo`” ou contenha "`bin`" ou "`lib`" conforme especificado no padrão.

### Máterial Complementar:
https://www.linuxforce.com.br/comandos-linux/comandos-linux-comando-tree/