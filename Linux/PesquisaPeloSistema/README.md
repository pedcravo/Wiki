# Comandos para Pesquisa pelo Sistema

Nesta sessão iremos ver os principais comandos para fazer pesquisas pelo sistema, seja para pesquisar comandos ou diretórios em todo o sistema.

### Comandos:
1. [`apropos`](#apropos)
2. [`dmesg`](#dmesg)
3. [`find`](#find)
4. [`inxi`](#inxi)
5. [`journalctl`](#journalctl)
6. [`locate`](#locate)
7. [`ls`](#ls)
8. [`lscpu`](#lscpu)
9. [`lsmod`](#lsmod)
10. [`lsof`](#lsof)
11. [`lspci`](#lspci)
12. [`lsusb`](#lsusb)
13. [`netstat` e `ss`](#netstat-e-ss)
14. [`pvdisplay`](#pvdisplay)
15. [`sar`](#sar)
16. [`ss`](#ss)

## `apropos`
### Para que serve?
Utilizado para **pesquisar palavras-chave** nas descrições das páginas de manual no sistema Linux. O comando `apropos` ajuda a encontrar **comandos e suas descrições associadas que correspondem a uma determinada palavra ou expressão regular**, exibindo os resultados relevantes encontrados no `man`.

> É muito útil quando você sabe o que um comando faz, mas não lembra o nome exato dele, permitindo pesquisar por funções ou termos relacionados.

### Opções:
- `-a` → Exibe resultados que correspondam a todas as palavras-chave fornecidas.
- `-e` → Busca exata. Procura pela palavra-chave exatamente como ela foi digitada, correspondendo ao nome completo ou descrição.
- `-l` → Evita que a saída seja cortada para se ajustar à largura do terminal.
- `-r` → Interpreta a palavra-chave como uma expressão regular (configuração padrão).
- `-s N` → Pesquisa em seções específicas do manual, seções de número `N`.
- `-v` → Modo detalhado, exibe mais informações durante a execução, útil para depuração.
- `-w` → Interpreta a palavra-chave como um padrão com curingas (`?`, `*`).

### Sintaxe comum:
**`$ apropos [OPÇÕES] PALAVRA-CHAVE`**

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

---

## `dmesg`
### Para que serve?
É utilizado para **visualizar todas as mensagens de hardware do sistema, a partir do momento da inicialização.**
Semelhante ao `journalctl`, porém é mais voltado para o hardware.

> Comando usado apenas com `sudo`.

### Exemplos:
`# dmesg | less` → Usa o `less` para visualizar todas as mensagens de hardware do sistema, a partir do momento da inicialização.
`# dmesg | less | grep RAM` → Utiliza o `grep` para filtrar as mensagens do `dmesg` e visualiza elas através do `less`.

---

## `find`
### Para que serve?
Utilizado para encontrar arquivos e diretórios com base em vários atributos (nome, tipo, tamanho, permissões, data de modificação e muito mais)

> Comando funciona melhor com sudo.

### Opções:
- `.` → Todos os tipos de usuários.
- `/` → Local atual do sistema.
- `\` → Usado para colocar caracteres especiais “(”.
- `-name` → Pesquisa pelo nome.
- `-iname` → Pesquisa pelo nome sem diferenciar maiúscula da minúscula.
- `*.log` → Final *.log*.
- `*.txt` → Final *.txt*.
- `-type d` → Pesquisa diretórios.
- `-type f` → Pesquisa arquivos.
- `-size` → Pesquisa por tamanho.
- `+100M` → Arquivos maiores que *100Mb*.
- `+2G` → Arquivos maiores que *2Gb*.
- `-mtime` → Pesquisa por arquivos modificados nos últimos n dias.
- `-atime` → Pesquisa por arquivos acessados nos últimos n dias.
- `-ctime` → Pesquisa por arquivos com mudanças de permissões nos últimos n dias.
- `-ls` → Organiza em colunas.
- `-exec` → Executa outros comandos (`-exec COMANDO {} /; `).
- `{}` → É o nome do arquivo.
- `-user` → Pesquisa pelos usuários.
- `-perm` → Procura por permissões ou bugs no sistema.
### Sintaxe comum:
**`# find CAMINHO [OPÇÕES] ARQUIVO`**

### Exemplos:
`# find` → Mostra os arquivos do sistema a partir do local atual.

`# find . -name 'arquivo.txt’` → Mostra os arquivos a partir do diretório atual que tem o nome *arquivo.txt*.

`# find . -iname 'arquivo.txt’` → Mostra os arquivos a partir do diretório atual que tem o nome *arquivo.txt* sem ter diferença de maiúsculas para minusculas.

`# find / -type d -name 'documentos’` → Pesquisa diretórios com o nome documentos.

`# find / -type f -name "documentos"` → Pesquisa arquivos com o nome documentos.

`# find /var/log -type f -name "*.log"` → Pesquisa arquivos no */var/log* com o final *.log*.

`# find ./Downloads -type f -name "*.txt"` → Pesquisa arquivos no diretório *Downloads* com o final *.txt*.

`# find / -size +100M` → Pesquisa arquivos maiores que 100Mb.

`# find / -size +100M -size -200M` → Pesquisa arquivos maiores que 100Mb e menores que 200Mb.

`# find / -size +2G` → Pesquisa arquivos maiores que 2Gb.

`# find /var/log -mtime -7` → Pesquisa os arquivos alterados nos ultimos 7 dia.

`# find /bin /usr/bin /sbin /usr/sbin -ctime +3` → Pesquisa por arquivos dentro dos dos repositórios */bin*, */usr/bin*, */sbin* e */usr/sbin* que tiveram suas permissões alteradas a + de 3 dias.

`# find / -mmin -10` → Pesquisa os arquivos alterados nos ultimos 10 minutos.

`# find / -size +500M -size -5G -exec du -sh {} \;` → Procura os arquivos e diretórios maiores que 500Mb e menores que 5G  e mostra o tamanho de cada um executando `du`.

`# find /pictures -type f -name "*.jpg" -exec cp {} {}.backup \;` → Encontra os arquivos do diretório *pictures* com o final *.jpg* e cria uma copia do arquivo (cp) e acrescenta a estas cópias a extensão *.backup*.

`# find /images -type f -name "*.png" -exec convert {} {}.jpg \;` → Encontra os arquivos com final *.png* do diretório *images* e faz uma conversão para *jpg* colocando a extensão *.jpg* para cada arquivo.

`# find /home -user pedrocravo -ls` → Pesquisa pelo usuário *pedrocravo* no */home*.

`# find /home -not -user pedrocravo -ls` → Pesquisa pelos usuários que não sejam *pedrocravo*.

`# find /etc -group root -ls` → Procura pelos arquivos com o grupo do root.

`# find / -empty` → Encontra diretórios vazios.

`# find /usr/bin -perm -755 -ls` → Encontra todos os arquivos em */usr/bin* com permissões de *755*.

`# find /data/reports -type f -name "*.csv" -exec sh -c 'mv "$0" "$(dirname "$0")/$(date +%Y%m%d)-$(basename "$0")"' {} \;` → Este comando localiza os arquivos *.csv* e renomeia cada um prefixando a data atual, melhorando a organização de arquivos e o controle de versão.

### Máterial Complementar:
https://linehost.cloud/linux/como-usar-a-opcao-de-comando-find-exec-no-linux/#sintaxe-da-opcao-de-comando-find-execfind

---

## `inxi`
### Para que serve?
É utilizado para mostrar detalhes do hardware e alguns dados do software.

> É necessário instala-lo.

### Exemplos:
`$ sudo apt install inxi` → Instala inxi.

`$ sudo inxi -F` → Mostra todas as informações detalhadas do hardware e algumas do software.

---

## `journalctl`
### Para que serve?
O comando `journalctl` é um poderoso utilitário para **consultas e exibições de registros de eventos** (log files). Ele é um componente essencial do `systemd`, gerenciador de sistemas e serviços padrão de muitas distribuições modernas do Linux. 

Assim, ele faz referência à sua função de controlar e analisar registros do diário do sistema.

Uma das características mais úteis do `journalctl` é a sua capacidade de **filtrar entradas de registro com base em critérios.** Graças a esse recurso, você poderá buscar informações  relevantes de forma direcionada e, assim, identificar problemas mais rapidamente. A seguir, apresentaremos as opções de filtragem mais comuns do `journalctl`.

> **Alternativa Ontick:**
> 
> Salvar em arquivo de */log* e dar comando `tail`.

### Opções:
- `-b` → Exibe todas as entradas coletadas desde o `boot` mais recente.
- `--disk-usage` → É utilizado para verificar o quanto de espaço o jornal ocupa no sistema.
- `-f` ou `--follow` → É utilizado para exibir as mensagens em tempo real (saída semelhante ao `tail -f`).
- `--vacuum-size=N` → Reduz o jornal com base no tamanho definido com uma unidade de medida  (`K`, `M` ou `G`).
- `--vacuum-time=N` → Reduz o jornal estabelecendo um limite de tempo de armazenamento (vai apagar qualquer coisa que tenha mais de `N` tempo).

### Exemplos:
`$ journalctl --disk-usage` → Mostra quanto de espaço o jornal está ocupando atualmente no sistema.
`# journalctl --vacuum-size=1G` → Restringe o jornal ao tamanho de 1G e exclui o excedente ao limite.
`# journalctl` --vacuum-time=1years → Restringe o jornal a manter somente as mensagens de registro do último ano.
`$ journalctl -b` → Mostra as mensagens do jornal a partir do `boot` mais recente.
`$ journalctl -b 1` → Mostra a 1ª mensagem do jornal a partir do `boot` mais recente.

### Máterial Complementar:
https://www.ionos.com/pt-br/digitalguide/servidor/ferramentas/journalctl/

---

## `locate`
### Para que serve?
Utilizado para **pesquisar rapidamente arquivos e diretórios no sistema.**

O `locate` consulta um banco de dados que contém uma lista de arquivos e diretórios previamente indexados.

> Comando funciona melhor com `sudo`

### Opções:
- `-c` → Conta o número de ocorrências encontradas, em vez de exibir as linhas.
- `-e` → Mostra somente arquivos que realmente existem no sistema (evita arquivos que foram deletados após a última indexação).
- `-i` → Faz a pesquisa ignorando maiúsculas e minúsculas (case-insensitive).
- `-n` → Limita a saída para `n` resultados (exibe apenas os primeiros `n` resultados).
- `-r` → Usa expressões regulares para realizar uma busca mais avançada.

> `/home/.*\.txt$` → Todos os arquivos *.txt* dentro do */home*.

### Sintaxe comum:
**`# locate [OPÇÕES] ARQUIVO`**

### Exemplos:
`# locate .bashrc` → Pesquisa e mostra todos os arquivos e diretórios que tem *.bashrc*.

`# locate -i downloads` → Pesquisa e mostra todos os arquivos e diretórios com *downloads* ignorando a diferença entre as letras maiúsculas e minusculas.

`# locate -c downloads` → Pesquisa e conta os arquivos e diretórios que exitem no sistema.

`# locate -n 10 downloads` → Pesquisa e mostra somente as 10 primeiras linhas que correspondem a palavra downloads.

`# locate -r '/home/.*\.txt$'` → Pesquisa e mostra os aquivos que correspondem a expressão.

`# locate -e documento` → Mostra somente arquivos que existem atualmente no sistema e que correspondem a documentos.

`# updatedb` → Atualiza o banco de dados do locate.

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

## `lscpu`
### Para que serve?
Utilizado para **ver todos os detalhes da arquitetura da CPU**.

### Opções:
- `-x` ou `-parse` → Usa máscara hexadecimal para exibir as CPUs.
- `-h` ou `--help` → Exibe informações sobre o comando.
- `-V` ou `--version`→ Exibe a versão do aplicativo.

---

## `lsmod`
### Para que serve?
Utilizado para **ver os módulos de hardware carregados no Kernel.**

A saída do comando ira ser diversos Módulos com seus tamanhos e seus usos.

### Exemplos:
`/sbin/modinfo -d MOD` → É utilizado para pesquisar o `MOD` (nome do módulo) do sistema e ver seu nome completo, incluindo seu tipo.

`$ /sbin/modinfo -d cmac` → Pesquisa no sistema o módulo `cmac`, retorna seu nome e seu tipo: `CMAC keyed hash algorithm`.

---

## `lsof`
### Para que serve?
O comando `lsof` **lista os arquivos abertos no sistema operacional**, juntamente com as informações associadas a cada um deles: Caminhos, Processos, Usuários, Arquivo descritor,  Dono do processo.  
Anda junto com o comando `ss`.

> Este comando possui limitações quando executado por usuários com permissões comuns, então indicamos o seu uso com `root`.

### Estrutura de Saída:
- **COMMAND** → Nome do comando que abriu o arquivo.
-  **PID** → ID do processo.
-  **USER** → Nome do usuário que iniciou o processo.
-  **FD** → Descritor de arquivo (ex.: cwd para diretório de trabalho atual, txt para texto de programa).
-  **TYPE** → Tipo de arquivo (ex.: REG para arquivo regular, DIR para diretório).
-  **DEVICE** → Dispositivo associado ao arquivo.
-  **SIZE/OFF** → Tamanho ou deslocamento do arquivo.
-  **NODE** → Número do nó do arquivo.
-  **NAME** → Caminho completo do arquivo ou nome da rede.

### Opções:
- `^` → É utilizado antes do usuário ou nos demais nomes para receber a opção negada.
- `-a` → É a opção utilizada para fazer um `AND` com as demais opções, o padrão do comando é `OU`.
- `-c nome` → Filtra os processos pelo `nome`.
- `-i` → Lista todas as conexões de rede, como TCP e UDP. Pode especificar portas ou protocolos.
- `-i TCP:porta` → Lista processos em uma porta específica.
- `-i TCP:N-M` → Lista processos de um range de portas, de `N` a `M`.
- `-u usuário` → Lista arquivos abertos de um `usuário` específico.
- `-n` → Mostra os nomes em forma numérica.
- `-t` → Exibe somente os IDs dos processos, útil para encadear com outros comandos.
- `-p PID` → Pesquisa por um `PID` específico.
- `+D` → Lista arquivos que estão abertos  em um diretório específico, não verifica subdiretórios.
- `+r` ou `+d` → Lista arquivos abertos recursivamente, incluindo subdiretórios.

### Sintaxe comum:
**`# lsof [OPÇÕES]`**

### Exemplos:
`# lsof` → Lista todos os arquivos abertos.

`# lsof -i` → Lista todas as conexões de rede.

`# lsof /home/Downloads/arquivo.txt` → Mostra quais processos manipulam o arquivo indicado.

`# lsof /dev/log` → Mostra os processos que manipulam o arquivo */dev/log*, mostra os servidores de logs.

`# lsof -c bash -c zsh` → Mostra os processos que possuem as palavras *bash* e *zsh*.

`# lsof -a -u pedro -c bash` → Mostra os processos do usuário pedro que possuem a palavra chave *bash*.

`# lsof -u pedro` → Lista arquivos abertos do usuário *pedro*.

`# lsof -u pedro -c bash` → Mostra todos os processos do usuário *pedro* e todos que possuem a palavra chave *bash*.

`# lsof -u ^pedro` → Mostra os arquivos de todos os usuários, exceto os do usuário *pedro*.

`# lsof -t -c bash` → Mostra somente os `PID`s dos processos com nome *bash*.

`# lsof -t -a -u pedro -c bash` → Mostra os `PID`s dos processos com nome bash do usuário pedro.

`# lsof -t -a -u ^pedro -c bash` → Mostra os `PID`s dos processos com nome *bash* que não pertence ao usuário *pedro*.

`# lsof -p 170513` → Mostra apenas o processo com `PID` *170513*.

### Máterial Complementar:
https://blog.ironlinux.com.br/o-comando-lsof-no-linux/

https://www.youtube.com/watch?v=FaTlrHq8RKM

---

## `lspci`
### Para que serve?
É utilizado para mostrar e filtrar o barramento PCI do hardware no sistema.

### Exemplos:
`$ lspci` → Mostra todos os barramentos `PCI` do hardware.

`$ lspci| grep VGA` → Filtra os barramentos `PCI` do hardware procurando e mostrando apenas o `VGA`.

---

## `lsusb`
### Para que serve?
Utilizado para ver detalhes das portas USB.

### Opções:
- `-v`, `--verbose` → Mostra informações detalhadas.
- `-D device` → Exibe informações apenas do dispositivo especificado.
- `-V`, `--version` → Exibe informações sobre o aplicativo.
- `-h` ou `--help` → Exibe informações sobre o comando.

---

## `netstat` e `ss`

### Para que serve?
O `netstat` e seu sucessor, `ss`, são utilitários de rede **que exibem informações sobre conexões de rede, tabelas de roteamento, portas abertas, serviços ativos e estatísticas de pacotes.** O `netstat` foi amplamente utilizado por anos, mas foi descontinuado em algumas distribuições Linux em favor do `ss`, que oferece maior rapidez e detalhes nas informações de rede.

O comando `netstat` exibe informações sobre conexões de rede ativas, tabelas de roteamento, interfaces de rede, portas abertas, e estatísticas de pacotes. É útil para visualizar conexões TCP/UDP, monitorar quais portas estão em escuta e identificar serviços ou processos ativos associados a essas conexões.

O comando `ss` exibe sockets ativos e conexões de rede, com maior eficiência e desempenho que o `netstat`. Ele fornece dados mais rápidos sobre conexões e permite filtros detalhados para tipos de conexões específicas, como TCP, UDP e UNIX sockets.

### Comparação `netstat` vs. `ss`
- **Desempenho**: `ss` é mais rápido e eficiente que `netstat`, especialmente em sistemas com muitas conexões de rede.
- **Recursos de Filtro**: `ss` permite filtros avançados, como `dst`, `src`, `dport`, que ajudam a isolar informações específicas de uma conexão.
- **Tabela de Roteamento**: `netstat -r` exibe a tabela de roteamento diretamente, enquanto ss depende do comando `ip route` para essa funcionalidade.
- **Detalhamento de Estatísticas**: `ss -s` fornece um resumo detalhado de todas as conexões de rede, algo que não está presente diretamente no `netstat`.

### Opções:
<img src="https://github.com/pedcravo/Wiki/blob/main/Linux/netstatess1.png" width="600px">

### `netstat`
#### Sintaxe comum:
**`$ netstat [OPÇÕES]`**

#### Exemplos:
`$ netstat -nr` → Exibe tabela de roteamento exibindo endereços IP e portas em formato numérico.

`$ netstat -tuln` → Listar todas (inclusive em escuta) as conexões TCP e UDP em formato numérico.

`$ netstat -tulpn` → Listar todas (inclusive em escuta) as conexões TCP e UDP em formato numérico, incluindo PID e nome do programa.

`$ netstat -neopa` → Exibe endereços IP e portas em formato numérico, mostra informações adicionais, como UID de processos, juntamente com temporizadores para conexões, PID e o nome do programa associado a cada conexão de todas as conexões e portas de escuta (listening).

`$ netstat -g` → Mostra os grupos multicast.

`$ netstat -gn` → Mostra os grupos multicast em formato numérico.

`$ netstat -r` → Exibir tabela de roteamento do kernel.

`$ netstat -nr -6` → Exibir tabela de roteamento IPv6 do kernel com as portas em formato numérico.

### `ss`
#### Sintaxe comum ss:
**`$ ss [OPÇÕES]`**

#### Exemplos:
`$ ss -lt` → Lista todos os sockets TCP de escuta.

`$ ss -tulpn` → Listar todas (inclusive em escuta) as conexões TCP e UDP em formato numérico, incluindo PID e nome do programa.

`$ ss -neopa` → Exibe endereços IP e portas em formato numérico, mostra informações adicionais, como UID de processos, juntamente com temporizadores para conexões, PID e o nome do programa associado a cada conexão de todas as conexões e portas de escuta (listening).

`$ ss -s` → Exibir estatísticas detalhadas de sockets e conexões de rede.

### Máterial Complementar:
<img src="https://github.com/pedcravo/Wiki/blob/main/Linux/netstatess2.webp" width="600px">

---

## `pvdisplay`
### Para que serve?
O comando `pvdisplay` é usado para **exibir informações detalhadas sobre volumes físicos (PVs) no sistema que fazem parte do gerenciamento de volumes lógicos (LVM).** Ele fornece informações como tamanho total, tamanho alocado, grupo de volume associado e outras propriedades.

O pvdisplay faz parte do pacote lvm2, que é necessário para gerenciar volumes lógicos no Linux.

### Opções:
- `-C` → Exibe as informações no formato de tabela.
- `--units [s|b|k|m|g|t|p]` → Define a unidade de tamanho exibida: setores, bytes, kilobytes, megabytes, etc.
- `-v` → Ativa a saída detalhada.
- `--readonly` → Exibe as informações sem modificar nada no disco.

### Saída esperada
Um exemplo da saída do comando:
```bash
  --- Physical volume ---
  PV Name               /dev/sda2
  VG Name               myvg
  PV Size               100.00 GiB
  Allocatable           yes (but full)
  PE Size               4.00 MiB
  Total PE              25599
  Free PE               0
  Allocated PE          25599
  PV UUID               v1234-a567-89ef-gh01-ijklmnop
```

**Explicação:**
- **PV Name:** Nome do volume físico.
- **VG Name:** Nome do grupo de volume ao qual pertence.
- **PV Size:** Tamanho total do volume físico.
- **Allocatable:** Indica se é possível alocar espaço adicional no volume.
- **PE Size:** Tamanho das extensões físicas.
- **Total PE:** Número total de extensões físicas disponíveis.
- **Free PE:** Extensões físicas livres (não alocadas).
- **Allocated PE:** Extensões físicas já alocadas.
- **PV UUID:** Identificador único do volume físico.

### Sintaxe comum:
**`$ pvdisplay [OPÇÕES] [PV]`**

### Exemplos:
`$ pvdisplay` → Mostra informações como o tamanho total, tamanho usado, tamanho livre e o grupo de volume associado.

`$ pvdisplay /dev/sda2` → Detalha informações apenas para o volume físico */dev/sda2*.

`$ pvdisplay -C` → Mostra os volumes físicos de forma resumida e organizada em formato de tabela.

### Comandos relacionados:
- **`pvcreate`** → Cria um novo volume físico.
- **`pvremove`** → Remove um volume físico.
- **`vgdisplay`** → Exibe informações sobre grupos de volume (VGs).
- **`lvdisplay`** → Exibe informações sobre volumes lógicos (LVs).
- **`pvs`** → Exibe informações resumidas sobre volumes físicos.
- **`pvcreate`** → Cria um novo volume físico.
- **`pvremove`** → Remove um volume físico.
- **`vgdisplay`** → Exibe informações sobre grupos de volume (VGs).
- **`lvdisplay`** → Exibe informações sobre volumes lógicos (LVs).
- **`pvs`** → Exibe informações resumidas sobre volumes físicos.

### Máterial Complementar:
https://www.youtube.com/watch?v=vOSk7O1z_VE&list=TLPQMTExMTIwMjQlXIbVLj9UpQ&index=3

---

## `sar`
### Para que serve?
O comando `sar` (**System Activity Reporter**) é usado para **monitorar o desempenho do sistema em tempo real ou para exibir relatórios históricos de uso de recursos como CPU, RAM, SWAP, disco e rede.** Ele é parte do pacote *sysstat* e ajuda os administradores de sistemas a diagnosticar problemas de desempenho e analisar o uso dos recursos.

### Opções:
- `-u` → Mostra a utilização da CPU, incluindo tempo ocioso, tempo de usuário e tempo de sistema.
- `-r` → Exibe informações sobre a memória RAM, como livre, usada e buffers/caches.
- `-S` → Mostra o uso da memória SWAP.
- `-d` → Monitora o desempenho de discos, como leituras e gravações por segundo.
- `-n` → Analisa a largura de banda e conexões de rede. Use subopções como `DEV` (dispositivos de rede) para detalhar.
- `-o` → Grava os dados coletados em um arquivo para análise posterior.
- `-f` → Lê dados históricos de um arquivo salvo.
- `-b` → Mostra estatísticas básicas de E/S do sistema.
- `-q` → Estatísticas de filas de execução e carga do sistema.

### Sintaxe comum:
**`$ sar [OPÇÕES] INTERVALO CONTAGEM`**
- **INTERVALO:** Intervalo de tempo (em segundos) entre cada coleta.
- **CONTAGEM:** Número de vezes que o relatório será gerado.

### Exemplos:
`$ sar -u 1 1 | grep -v “Linux”` → Exibe o uso da CPU por 1 segundo e finaliza.

`$ sar -r 1 1 | grep -v “Linux”` → Mostra o uso de memória RAM (livre, usada e em cache).

`$ sar -S 1 1 | grep -v “Linux”` → Exibe informações sobre o uso da memória SWAP.

`$ sar -d 1 1 | grep -E “(DEV|sd|vd)” | grep -v “Linux”` → Mostra estatísticas de leitura e gravação em dispositivos como discos (ex.: `sdX` ou `vdX`).

`$ sar -n DEV 1 1 | grep -v lo | grep -v “Linux”` → Exibe o tráfego de dispositivos de rede, excluindo a interface `lo` (loopback).

`$ sar -o /tmp/sar_data 1 5` → Salva os dados coletados no arquivo */tmp/sar_data*.

`$ sar -f /tmp/sar_data` → Lê e exibe os dados coletados previamente salvos no arquivo */tmp/sar_data*.

`$ sar -u 1 1 | grep -v "Linux"` → Mostra estatísticas de CPU excluindo as linhas relacionadas ao kernel.

---

## `ss`
### Para que serve?
O comando `ss` (**Socket Statistics**) é usado para **exibir informações detalhadas sobre conexões de rede**. Ele substitui o antigo `netstat` e oferece uma maneira rápida e eficiente de monitorar e gerenciar sockets de rede.

> Anda junto com o comando `lsof`.

### Arquivos Relacionados:
• */proc/net/tcp* e */proc/net/udp*: Contêm informações sobre conexões TCP e UDP ativas, usadas pelo `ss` para mostrar dados.
• */proc/net/unix*: Lista sockets Unix ativos.

### Opções:
- `-a` → Exibe todas as conexões, incluindo as que estão em estado de espera (**padrão**).
- `-i` → Mostra estatísticas de interface de rede.
- `-l` → Mostra apenas conexões em estado de escuta.
- `-n` → Exibe endereços e portas numéricos em vez de nomes simbólicos (**padrão**).
- `-o` → Exibe mais informações sobre cada conexão.
- `-p` → Exibe o processo associado a cada conexão.
- `-r` → Exibe informações sobre as rotas da rede (forma contrária ao `-n`)
- `-s` → Exibe um resumo estatístico das conexões por protocolo.
- `-t` → Mostra estatísticas de conexões TCP.
- `-u` → Mostra estatísticas de conexões UDP.
- `-4` e `-6` → Mostra apenas conexões IPv4 e IPv6, respectivamente.

### Estrutura da saída:
- Netid: O tipo de socket ou protocolo usado. (`tcp`, `udp`, `unix`, `nl`)
- **State**: Estado da conexão. Comum para conexões TCP (`ESTAB`, `LISTEN`, `CLOSE-WAIT`, `TIME-WAIT`).
- **Recv-Q** e **Send-Q**: Fila de recebimento (Recv-Q) e fila de envio (Send-Q):
- **Local Address**: Endereço IP local associado ao socket e porta locais.
- **Peer Address**: Endereço e porta do "peer" ou do lado remoto da conexão.

### Sintaxe comum:
**`# ss [OPÇÕES]`**

### Exemplos:
`$ ss -tul` → Exibe conexões de escuta TCP (`-t`) e UDP (`-u`) com IPs e portas sem resolver.

`$ ss -ta state established` → Mostra todas (`-a`) as conexões TCP ativas que estão estabelecidas.

### Máterial Complementar:
https://www.linkedin.com/pulse/explorando-o-comando-ss-linux-uma-vis%C3%A3o-detalhada-crestani-l%C3%B3pez-hxdsf/

https://www.youtube.com/watch?v=BreC2wBn250

https://www.youtube.com/watch?v=FaTlrHq8RKM