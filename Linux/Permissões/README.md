# Comandos para gerenciamento de Permissões

Nesta sessão iremos ver os principais comandos para gerenciamento de permissões.

### Comandos:

1. [`acl`](#acl)
2. [`chgrp`](#chgrp)
3. [`chmod`](#chmod)
4. [`chown`](#chown)

## `acl`

### Para que serve?
Os comandos `setfacl` e `getfacl` são usados para manipular e visualizar **ACLs** (Access Control Lists) no Linux, que permitem **gerenciar permissões detalhadas de arquivos e diretórios para usuários e grupos específicos**, além dos esquemas tradicionais de permissão (usuário, grupo, outros).

- `setfacl` → Configura permissões adicionais para usuários ou grupos específicos em um arquivo ou diretório.
- `getfacl` → Exibe as permissões ACL aplicadas a um arquivo ou diretório.

O uso de ACLs é útil para situações em que o sistema tradicional de permissões de leitura, escrita e execução (rwx) não é suficiente, permitindo a atribuição de permissões detalhadas para diferentes usuários e grupos.

Instalar pacote acl → `$ sudo apt install acl`.

### set
#### Opções:
- `-m` → Modifica permissões para o usuário ou grupo indicado.
- `-x` → Remove permissões para um usuário ou grupo específico.
- `-b` → Remove todas as entradas de ACL do arquivo ou diretório (limpa as permissões ACL).
- `-R` → Aplica as permissões recursivamente em diretórios e seus arquivos/subdiretórios.
- `-d` → Define permissões ACL padrão para um diretório, que serão herdadas por arquivos e subdiretórios criados posteriormente.
- `u` → Especifica que a ACL será aplicada a um usuário.
- `g` → Especifica que a ACL será aplicada a um grupo.

#### Sintaxe comum:
**`$ setfacl [OPÇÕES] u/g:USUÁRIO/GRUPO:rwx ARQUIVO`**

#### Exemplos:
`$ setfacl -m u:pedro:rx Downloads/arquivo.txt` → Muda as permissões do usuário `pedro` para `r` e `x` no arquivo `Downloads/arquivo.txt`.

`$ setfacl -m g:backend:rw /tmp/memo.txt` → Muda as permissões do grupo `backend` para `r` e `w` no arquivo `/tmp/memo.txt`.

`$ setfacl -m d:u:pedro:rw /tmp/backend/` → Cria um diretório com configurações padrões, qualquer subdir vai seguir as mesmas permissões.

### get
#### Opções:
- `-p` → Exibe as permissões ACL de um arquivo ou diretório, incluindo permissões padrão e permissões explícitas para usuários e grupos.
- `-R` → Exibe as permissões ACL de forma recursiva para todos os arquivos e subdiretórios de um diretório.

#### Sintaxe comum:
**`$ getfacl [OPÇÕES] ARQUIVO`**

#### Exemplos:
`$ getfacl -p /Downloads/arquivo.txt` → Mostra na tela uma série de permissões dos grupos em relação ao arquivo `Downloads/arquivo.txt`.

### Máterial Complementar:
https://link;comum.com.br/

---

## `chgrp`

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

## `chmod`

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

## `chown`

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