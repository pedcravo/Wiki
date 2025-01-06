
# Comandos para Manipulação de Arquivos
Nesta seção, exploramos comandos que permitem manipular arquivos e diretórios no Linux. Esses comandos são essenciais para **copiar, mover, alterar permissões, criar e remover arquivos e diretórios**.

### Comandos:

1. [`chgrp`](#chgrp)
2. [`chmod`](#chmod)
3. [`chown`](#chown)
4. [`cp`](#cp)
5. [`dd`](#dd)
6. [`expand`](#expand)
7. [`unexpand`](#unexpand)
8. [`ln`](#ln)
11. [`mv`](#mv)
12. [`paste`](#paste)
13. [`rm`](#rm)
9. [`mkdir`](#mkdir)
10. [`rmdir`](#rmdir)
14. [`split`](#split)
15. [`touch`](#touch)

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

---

## `cp`

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
https://www.certificacaolinux.com.br/comando-linux-cp/

https://labex.io/tutorials/linux-linux-cp-command-file-copying-209744

---

## `dd`

### Para que serve?

### Opções:

### Sintaxe comum:
**`$ dd if=ORIGEM of=DESTINO [OPÇÕES]`**

### Exemplos:

### Máterial Complementar:
https://www.linuxdescomplicado.com.br/2016/11/alguns-exemplos-de-que-o-comando-dd-pode-ser-considerado-umas-das-ferramentas-mais-versateis-do-linux.html

https://www.certificacaolinux.com.br/backup-do-mbr-com-o-comando-dd/

---

## `expand`

### Para que serve?
O comando `expand` é utilizado para **converter tabs em espaços** em um arquivo e quando nenhum arquivo é especificado, ele lê a partir da entrada padrão.

É interessante seu uso em scripts, para programadores é um comando excelente.

### Opções:
- `-i` → Converte apenas tabs iniciais, deixando tabs após espaços intactos.
- `-t N` → Define o número N de espaços que cada tabulação representará, com o padrão sendo 8.
- `-t LIST` → Define uma lista de posições de tabulação específicas separadas por vírgulas.

### Sintaxe comum:
**`$ expand [OPÇÕES] ARQUIVO`**

### Exemplos:
`$ expand arquivo.txt` → Converte todas as tabs para 8 espaços.

`$ expand --tabs=10 arquivo.txt > arquivo2.txt` → Converte cada tabs em 10 espaços e grava em arquivo2.txt.

`$ expand -t 4 -i documento.txt` → Converte apenas os tabs iniciais do arquivo para 4 espaços.

### Máterial Complementar:
https://www.linuxforce.com.br/comandos-linux/comandos-linux-comando-expand/

https://www.certificacaolinux.com.br/comando-linux-expand/

---

## `unexpand`

### Para que serve?
O comando `unexpand` é utilizado para **converter espaços em tabs em arquivos** de texto ou entrada padrão.

Esse comando é especialmente útil para reduzir o tamanho de arquivos que possuem grandes quantidades de espaços.

### Opções:
- `-a` → Converte todos os grupos de espaços em tabs, não apenas aqueles no início da linha.
- `--first-only` → Converte apenas os grupos iniciais de espaços em cada linha, padrão.
- `-t N` → Define a quantidade de espaços que um tab representa. O padrão é 8 espaços.
- `-t LIST` → Usa uma lista de posições separadas por vírgula para definir onde as tabulações devem ser colocadas.

### Sintaxe comum:
**`$ unexpand [OPÇÕES] ARQUIVO`**

### Exemplos:
`$ unexpand arquivo.txt` → Converte os espaços iniciais de cada linha em tabs.

`$ unexpand -a arquivo.txt` → Converte todos os espaços em tabs no arquivo inteiro.

`$ unexpand -t 4 arquivo.txt > arquivo_tabs.txt` → Converte grupos de 4 espaços em tabulações e grava no `arquivo_tabs.txt`.

`$ unexpand --tabs=4,8,12 arquivo.txt` → Usa posições de tabulação específicas para conversão, nos pontos definidos pela lista (4, 8 e 12).

### Máterial Complementar:
https://www.linuxforce.com.br/comandos-linux/comandos-linux-comando-expand/

https://www.certificacaolinux.com.br/comando-linux-expand/

---

## `ln`

### Para que serve?
O comando `ln` (Link) é utilizado para **criar links para arquivos ou diretórios no sistema Unix**, similar ao conceito de “atalho” em outros sistemas operacionais.

#### Tipos de Link
-  **Link Direto (Hard Link)** → Adiciona um novo nome para o mesmo arquivo (compartilha o mesmo inode). O arquivo só é removido do sistema quando o último link para ele é deletado. É uma referência direta ao conteúdo do arquivo.

- **Link Simbólico (Soft Link ou Symlink)** → Aponta para o caminho de um arquivo ou diretório (possui um inode próprio). É possível criar links simbólicos para arquivos em diferentes sistemas de arquivos ou diretórios, e o link permanece mesmo que o arquivo de destino seja excluído.

### Opções:
- `-d` → Cria um link direto, é o padrão.
- `-L` → Cria uma link para um link simbólico.
- `-s` → Cria uma link simbólico.
- `-t DIR` → Especifica o diretório `DIR` destino.
- `-v` → Mostra o nome de cada arquivo antes de criar o link.

### Sintaxe comum:
`$ ln [OPÇÕES] ORIGEM DESTINO`

### Exemplos:
`$ ln arquivo.txt linkdireto.txt` → Cria um link direto para `arquivo.txt` com o nome `linkdireto.txt`.

`$ ln -s /diretorio/exemplo linkexemplo` → Cria um link simbólico chamado `linkexemplo` para o diretório `/diretorio/exemplo`.

`$ ln -t /destino arquivo1 arquivo2` → Cria links diretos para `arquivo1` e `arquivo2` no diretório `/destino`.

`$ ln -s -v pasta_original/ pasta_link/` → Cria um link simbólico para `pasta_original` com o nome `pasta_link` e exibe o progresso.

### Máterial Complementar:
https://guialinux.uniriotec.br/ln/

---

## `mv`

### Para que serve?
O comando `mv` é utilizado para **mover ou renomear arquivos e diretórios**. Pode ser movido mais de um arquivo ou diretório ao mesmo tempo

Ficar atento a arquivos de mesmo nome, um arquivo sobrepõe outro sem perguntar.

### Opções:
- `-f` → Força a substituição dos arquivos existentes sem avisar.
- `-i` → Realiza checagem de segurança.
- `-n` → Não permite a sobrepoisção de arquivos.
- `-v` → Mostra na tela as ações executadas.

### Sintaxe comum:
**`$ mv [OPÇÕES] ARQUIVO.. DESTINO`**

### Exemplos:
`$ mv arquivo.txt ~/Downloads` → Move um arquivo para o diretório `Downloads`, a partir de qualquer diretório.

`$ mv arquivo1.txt arquivo2.txt Downloads/` → Move dois arquivos para o diretório `Downloads` a partir do `/home`.

`$ mv *.txt /Downloads/` → Move todos os arquivos `.txt` para o diretório `Downloads`.

`$ mv *.txt Downloads` → Move todos os arquivos com `.txt` para o diretório `Downloads`.

`$ mv arquivo.txt renomeado_arquivo.txt` → Renomeia o arquivo, utilizar o mesmo final `.txt`.

`$ mv Dir/ DirRenomeada/` → Renomeia um diretório no mesmo local em que estava o original.

`$ mv -i arquivo.txt Downloads` → Checa se tem arquivos com mesmo nome no local de destino.

`$ mv -n arquivo.txt Downloads` → Move um ou mais arquivos sem permitir a sobreposição no local de destino, neste caso `Downloads`.

`$ mv -v arquivo diretorio` → Move um arquivo mostrando na tela o caminho do que foi feita.

### Máterial Complementar:
https://labex.io/tutorials/linux-linux-mv-command-file-moving-and-renaming-209743

https://www.linuxforce.com.br/comandos-linux/comandos-linux-comando-mv/

---

## `paste`

### Para que serve?
O comando `paste` é utilizado para **unir dois arquivos tanto na tela quanto em um novo arquivo novo**.

### Opções:
- `-d` → Define um separador.
- `-s` → Troca a organização dos arquivos para uma coluna única.

### Sintaxe comum:
**`$ paste [OPÇÕES] ARQUIVO…`**

### Exemplos:
`$ paste arquivo1.txt arquivo2.txt` → Une linhas de arquivos lado a lado separador por tab.

`$ paste -d "," arquivo1.txt arquivo2.txt` → Une dois arquivos na tela e os separa com `,`.

`$ paste -s arquivo1.txt arquivo2.txt` → Une dois arquivos em somente uma coluna, um arquivo sobre o outro.

`$ paste arquivo1.txt arquivo2.txt > combinacao.txt` → Une dois arquivos em um aquivo novo.

### Máterial Complementar:
Não possui material complementar.

---

## `rm`

### Para que serve?
O comando `rm` é utilizado para **remover arquivos e diretórios cheios**. Pode ser removido mais de um arquivo ou diretório ao mesmo tempo.

### Opções:
- `-f` → Força a remoção.
- `-i` → Faz checagem de segurança.
- `-r` → Faz a remoção de diretório.

### Sintaxe comum:
**`$ rm [OPÇÕES] ITEM`**

### Exemplos:
`$ rm exemploarquivo.txt` → Remove arquivo.

`$ rm -r exemplopasta` → Remove diretório exemplopasta recursivamente, remove ele e tudo que tem dentro (diretórios e arquivos).

`$ rm -i arquivo.txt` → Questiona se realmente é para apagar a pasta.

`$ rm -f arquivo.txt` → Força a remoção do arquivo.

`$ rm -r exemplopasta` → Remove um diretório.

`$ rm -rf exemplopasta` → Força a remoção do diretório `exemplopasta` recursivamente.

### Máterial Complementar:
https://labex.io/tutorials/linux-linux-rm-command-file-removing-209741

---

## `mkdir`

### Para que serve?
O comando mkdir é utilizado para criar um ou mais diretórios.

### Opções:
- `-p` → Permite criar diretórios pais e filhos.
- `-v` → Mostra na tela as ações sendo executadas.

### Sintaxe comum:
**`$ mkdir [OPÇÕES] NOME_DIRETÓRIO`**

### Exemplos:
`$ mkdir exemplopasta` → Cria um diretório no local atual.

`$ mkdir dir1 dir2` → Cria 2 diretórios no local atual.

`$ mkdir /home/pedrocravo/Documentos/exemplopasta` → cria diretório no local `/home/pedrocravo/Documentos`.

`$ mkdir -p dirpai/dirmeio/dirfilho` → Cria diretórios em cadeia.

`$ mkdir -pv dirpai/dirmeio/dirfilho` → Cria diretórios em cadeia e mostra na tela o que está sendo feito.

### Máterial Complementar:
Não possui material complementar.

---

## `rmdir`

### Para que serve?
O comando `rmdir` é utilizado para **remover um ou mais diretórios vazios**.

### Opções:
- `-p` → Remove uma hierarquia de diretórios (recursivamente).
- `-v` → Exibe informações para cada diretório processado.

### Sintaxe comum:
**`$ rmdir [OPÇÕES] DIRETÓRIO...`**

### Exemplos:
`$ rmdir exemplopasta` → Remove diretório no local.

`$ rmdir dir1 dir2` → Remove dois diretórios no local.

`$ rmdir /home/pedrocravo/Documentos/exemplopasta` → Remove diretório no local `/home/pedrocravo/Documentos`.

`$ rmdir --ignore-fail-on-non-empty exemplopasta` → Remove diretório no local ignorando arquivos dentro dele.

### Máterial Complementar:
https://guialinux.uniriotec.br/rmdir/

---

## `split`

### Para que serve?
O comando `split` é utilizado para **dividir arquivos grandes em arquivos menores**, com base no número de linhas ou no tamanho em bytes. Esse comando é útil para processar ou transferir arquivos grandes em partes menores.

- O padrão é dividir o arquivo a cada **1000 linhas**.
- Os nomes dos arquivos de saída seguem o padrão arquivo**aa**, arquivos**ab**, arquivo**ac**, assim por diante. É possível especificar um sufixo para o arquivo de saída.

### Opções:
- `-a N` → Define o comprimento dos sufixos em `N` caracteres.
- `-b N` → Divide o arquivo em um número `N` de bytes.
- `-d` → Usa números como sufixos no lugar de letras.
- `-l N` ou `-N` → Onde `N` é o número de linhas que irão dividir o arquivo de entrada.

### Sintaxe comum:
**`$ split [OPÇÕES] ARQUIVO PREFIXO`**

### Exemplos:
`$ split -2 arquivo.txt lista_` → Divide o arquivo a cada 2 linhas, cada arquivo menor vai ter 2 linhas.

`$ split -a 3 -l 2 arquivo.txt parte_` → Divide arquivo em arquivos de 2 linhas cada, usando sufixos de 3 caracteres.

`$ split -b 1M arquivo.txt parte_` → Divide o arquivo em arquivos de 1 megabyte cada.

`$ split -b 1K arquivo.txt parte_` → Divide arquivo em arquivos de 1 KB cada.

`$ split -d -l 3 arquivo.txt parte_` → Divide arquivo em arquivos de 3 linhas cada, usando sufixos numéricos.

`$ split -d -a 3 -l 100 arquivo.txt parte_` → Divide arquivo em arquivos de 100 linhas cada, usando sufixos numéricos de 3 dígitos.

### Máterial Complementar:
https://www.certificacaolinux.com.br/comando-linux-split/

---

## `touch`

### Para que serve?
O comando `touch` é utilizado para **criar arquivos em branco ou atualizar a data e hora de modificação e acesso de arquivos existentes**. É uma maneira rápida de criar arquivos vazios ou ajustar os timestamps de arquivos.

É possível criar **mais de um arquivo ao mesmo tempo**, e caso o arquivo já exista, o `touch` não modifica seu conteúdo, apenas altera suas informações de data e hora.

### Opções:
- `-a` → Atualiza apenas o horário de acesso do arquivo, sem modificar o horário de modificação
- `-c` → Não cria o arquivo caso ele não exista. Apenas modifica a data e hora de arquivos que já existem.
- `-m` → Atualiza apenas o horário de modificação do arquivo, sem alterar o horário de acesso.
- `-r` → Usa o timestamp de outro arquivo para definir a data e hora de modificação do arquivo.
- `-t` → Define uma data e hora específicas para o arquivo, no formato [[CC]YY]MMDDhhmm[.ss] (ano, mês, dia, hora, minuto e segundos opcionais).

### Sintaxe comum:
**`$ touch [OPÇÕES] ARQUIVO`**

### Exemplos:
`$ touch arquivo` → Cria um arquivo comum.

`$ touch arquivo.txt` → Cria um arquivo `.txt`.

`$ touch .arquivo` → Cria um arquivo oculto.

`$ touch arquivo1.txt arquivo2.txt` → Cria dois arquivos `.txt`.

`$ touch -a arquivo.txt` → Atualiza a data de acesso de `arquivo.txt` sem modificar seu conteúdo.

`$ touch -t 202401011200 arquivo.txt` → Define a data e hora de `arquivo.txt` para 1º de janeiro de 2024, 12:00.

`$ touch -r modelo.txt novoarquivo.txt` → Copia a data e hora do arquivo `modelo.txt` para o arquivo `novoarquivo.txt`.

### Máterial Complementar:
Não possui material complementar.