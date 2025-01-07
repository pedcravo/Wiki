# Comandos de manipulação do sistema

Nesta sessão vamos ver os comandos que são utilizados para manipular o sistema, ou seja, os comandos que mexem nas configurações do sistema e dos processos.

### Comandos:

1. [`&`](#&)
2. [`at`](#at)
3. [`bg`](#bg)
4. [`fg`](#fg`)
5. [`cron` e `anacron`](#cron-e-anacron)
6. [`date`](#date)
7. [`fdisk`](#fdisk)
8.  [`free`](#free)
9.  [`history`](#history)
10. [`iostat`](#iostat)
11. [`iperf`](#iperf)
12. [`jobs`](#jobs)
13. [`kill`](#kill)
14. [`mii-tool` e `ethtool`]()
15. [`modprobe`]()
16. [`mount` e `unmount`]()
17. [`nice`](#nice)
18. [`ionice`](#ionice)
19. [`renice`]()
20. [`nmcli` e `nmtui`]()
21. [`pgrep`]()
22. [`ps`]()
23. [`pstree`]()
24. [`sftp`]()
25. [`ssh`]()
26. [`swapon`]()
27. [`systemctl`]()
28. [`tmux`]()
29. [`top`](#top)
30. [`htop`](#htop)
31. [`tty`]()
32. [`tzselect`]()
33. [`uname`]()
34. [`uptime`]()
35. [`vmstat`]()

## `&`

### Para que serve?
Utilizado para executar comandos em segundo plano.
Pode ser substituído por Ctrl + Z .

### Sintaxe comum:
**`$ COMANDO & COMANDO`**

### Exemplos:
`$ tar ~/Downloads/arquivo.txt &` → executa comando em segundo plano

`$ find /usr > /tmp/allusrfiles &` → Executa o processo em segundo plano (adiciona na fila de execução de processos em segundo plano.

`$ sleep 10000 &` → Executa o processo em segundo plano (adiciona na fila de execução de processos em segundo plano.

---

## `at`

### Para que serve?
O comando `at` é utilizado para **agendar a execução de tarefas no futuro.** Ao contrário do `cron`, ele é ideal para agendamentos únicos, como executar um comando ou script em um horário ou data específica.
Facilitar o planejamento de tarefas pontuais sem precisar editar arquivos de configuração como no `cron`.

### Opções:
- `Ctrl + d` → Finaliza a entrada de comandos no shell interativo do `at`.
- `-f ARQUIVO` → Agenda a execução de um script ou arquivo com comandos.
- `-M` → Envia um email ao usuário caso o comando agendado tenha uma saída padrão.
- `-m` → Envia um email ao usuário mesmo que não haja saída padrão do comando agendado.
- `-t TIMESTAMP` → Especifica o horário e a data no formato `AAAAMMDDHHmm` para agendamento.
- `batch` ou `at -b` → Executa tarefas agendadas quando o sistema estiver ocioso (com baixa carga).
- `atq` → Exibe a lista de tarefas agendadas para o usuário atual.
- `atrm` ou `at -d` → Remove uma tarefa agendada pelo número do job.

### Sintaxe comum:
**`$ at [OPÇÕES] HORÁRIO`**

### Exemplos:
`# at 09:00` → Abre um novo shell para mandar comandos que serão executados no /bin/sh as 9hrs, criando um job.

`# echo “Comando a ser executado” | at 09:00` → Agenda comando `echo` para as 9hrs.

`# at 09:00 -f /root/script.sh` → Agenda a execução do `/root/script.sh` para as 9hrs.

`# at sunday +10 minutes` → Agenda a ação para o próximo domingo 10 minutos depois do horário atual.

`# at 1pm + 2 days` → Agenda a execução para as 13hrs daqui a dois dias.

`# at 12:30 012025` → Agenda comando para o dia 20/01/2025 as 12:30, sistema `MMDDAA`.

`# at now + 1 hour` → Agenda para o dia atual com o horário atual + 1hr.

`# at -t 202501201230` → Agenda a execução para o dia 20/01/2025 as 12:30, sistema `AAAAMMDDHHmm`.

---

## `bg`

### Para que serve?
O comando `bg` (background) no Linux é utilizado para **colocar um processo em segundo plano.** Isso é útil para continuar a execução de um processo que foi pausado (por exemplo, ao usar `Ctrl+Z`) sem ocupar o terminal.

Quando você pausa um processo com `Ctrl+Z`, ele fica suspenso, mas ainda ativo na lista de tarefas. Usar `bg` permite que esse processo continue rodando em segundo plano, liberando o terminal para outros comandos.

### Sintaxe comum:
**`bg [número_do_job]`**

### Exemplos:
`$ bg` → Retoma em segundo plano o processo com prioridade `+` (o ultimo a ser adicionado).
`$ bg %1` → Retoma em segundo plano o processo de número 1 da fila.

### Máterial Complementar:
https://link;comum.com.br/

---

## `fg`

### Para que serve?
O comando `fg` (foreground) no Linux é **utilizado para trazer um processo que está rodando em segundo plano ou suspenso de volta para o primeiro plano**, o que significa que ele passa a ocupar o terminal atual.

Quando um processo está em segundo plano ou pausado, ele não utiliza o terminal de entrada diretamente. Com `fg`, esse processo é trazido de volta para ser executado diretamente no terminal, permitindo uma interação direta com o processo.

**Sem Argumento:** `fg` sem argumentos trará o job mais recente para o primeiro plano.

### Sintaxe comum:
**`fg [número_do_job]`**

### Exemplos:
`$ fg` → Retoma em primeiro plano o processo com prioridade `+`.

`$ fg %1` → Retoma em primeiro plano o processo número 1.

`$ fg %2` → Retoma em primeiro plano o processo número 2.

### Máterial Complementar:
https://link;comum.com.br/

---

## `cron` e `anacron`

### Para que serve?
São daemons, programas de segundo plano que procuram situações ou ações para entrar em ação. **Eles agendam a execução de comandos.**
Utilizados para **executar ações repetitivas, diárias ou continuas.**

`cron` → Geralmente utilizado em servidores. (24h/7)
`anacron` → Muito utilizado em desktop. Faz uma fila de pendências, executa somente quando a máquina estiver ligada.

Funcionamento `cron`:
 ```
 .---------------- minute (0 - 59) → Minuto em que vai ser ativado.
 |   .------------- hour (0 - 23) → Hora em que vai ser ativado.
 |   |   .---------- day of month (1 - 31) → Dia em que vai ser ativado.
 |   |   |   .------- month (1 - 12) OR jan,feb,mar,apr ... → Mês em que vai rodar.
 |   |   |   |   .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu, → Dia da semana em que vai rodar.
 |   |   |   |   |
 *   *   *   *   * USUÁRIO COMANDO
```

`@yearly` (or `@annually`) → `0 0 1 1 *`
`@monthly` → `0 0 1 * *`
`@weekly` → `0 0 * * 0`
`@daily` (or @`midnight`) → `0 0 * * *`
`@hourly` → `0 * * * *`
`@reboot` → `N/A`

Funcionamento `anacron`:
`RANDOM DELAY=45` → Delay máximo que pode ser adicionado
`START_HOURS_RANGE=3-22` → Intervalo de tempo em que os trabalhos serão executados, horário de inicio-fim.

### Exemplos:
#### cron
`# nano /etc/crontab` → Edita a tabela de cron, a lista de programas e suas especificações de repetição.

`# crontab -e` → Outra maneira de editar a tabela cron, padrão de usuário root.

**Código:**
`1 * * * * echo "Teste de Cron!"` → Roda o código pelo usuário root no minuto 1 de cada hora, de cada dia.

`30 15 * * * echo "Deu 15:30"` → Roda o código pelo usuário root as 15:30 todos os dias.

#### anacron:
`# nano /etc/anacrontab` → Edita a tabela de ações do anacron.

**Código:**
`@daily  10      example.daily   /bin/bash /root/backup.sh`

### Máterial Complementar:
<img src="https://github.com/pedcravo/Wiki/blob/main/Linux/cron1.png" width="600px">

<img src="https://github.com/pedcravo/Wiki/blob/main/Linux/cron2.png" width="600px">

https://github.com/pedcravo/Wiki/blob/main/Linux/Aula-8-Compreendendo-o-serviço-Cron.txt

---

## `date`

### Para que serve?
O comando `date` é utilizado para mostrar a data e hora atual.
É possível modificar a data com outros comandos, veremos a seguir.

### Opções:
- `-d string` → Mostra as horas em uma determinado formato
- `-u` → Mostra ou configura as horas no formato UTC (Coordinated Universal Time)
- `-s` → Configura as horas

### Exemplos:
`# date -s “18 Nov 2024 17:00:00”` → Altera manualmente a hora do computador para a que está entre aspas.

`# date -s “20250101 13:00:00”` → Troca a data para 01/01/2025 13hrs.

`# date -s “2025-05-10 16:30:00”` → Troca a data para 10/05/2025 16:30.

`# date +%T -s “20:00:00”` → Modifica somente o horário e mantém o dia através de expressão regular.

`# date +%H -s “2”` → Modifica somente a hora e mantém o dia através de expressão regular.

`$ date +'Hoje é %A, %d de %B de %Y, o %j dia do ano, as %H:%M'` → Mostra dia e hora no seguinte formato: `Hoje é Saturday, 02 de November de 2019, o 292 dia do ano, as 14:14`.

`$ date +%H:%M:%S` → Mostra data no formato `Hora:Minuto:Segundo`.


`# dpkg-reconfigure tzdata` → É utilizado para configurar a data e hora do sistema (abre uma aba e atualiza automaticamente).


`# timedatectl` → Mostra mais dados sobre o horário mundial.

`# timedatectl set-ntp true` → Ativa a atualização automática de horário.

`# timedatectl set-ntp false` → Desativa a atualização automática de horário.

`# timedatectl set-time 10:00:00` → Modifica apenas a hora do sistema.

`# timedatectl set-time 2025-05-01` → Modifica apenas a data do sistema.

`# timedatectl set-time '2025-05-01 12:30:00'` → Modifica a data e hora do sistema.

`# timedatectl list-timezones` → Mostra todas as timezones.

`# timedatectl set-timezone America/Sao_Paulo` → Altera a timezone do sistema.

### Máterial Complementar:
https://link;comum.com.br/

---

## `fdisk`

### Para que serve?
O `fdisk` é um comando de linha para **criar, modificar, excluir e visualizar partições em discos rígidos.** Ele funciona com tabelas de partição do tipo **DOS, BSD** e **SUN**. É útil para configurar partições no sistema, especialmente em configurações onde sistemas de arquivos tradicionais são utilizados, embora não suporte GPT (Tabela de Partição GUID) em discos grandes, para os quais outras ferramentas como `parted` são recomendadas.

`fdisk` é um programa orientado a menus, onde cada função é ativada por comandos específicos dentro do modo interativo. 

> Este comando funciona de forma mais completa se utilizado com o usuário root.

#### Arquivos e Configurações Relacionados:
- `/dev/sdX` → Dispositivos de disco padrão em sistemas Linux (e.g., `/dev/sda` para o primeiro disco).
- `/proc/partitions` → Arquivo que lista partições detectadas no sistema operacional.
- `/etc/fstab` → Define pontos de montagem e configurações para partições no sistema.

#### Avisos:
- **Perigo de perda de dados** → Ao usar comandos de manipulação de partições, como `d` para deletar e `w` para gravar alterações, qualquer erro pode resultar em perda de dados. Sempre faça backup antes de usar `fdisk`.
- **Compatibilidade** → Não se recomenda o `fdisk` para manipulação de discos GPT ou discos maiores, onde o comando `parted` é mais adequado.
- **Descarte de setores antigos** → Após usar `fdisk`, é comum que o sistema execute um comando `sync` para atualizar as tabelas de partição.

### Opções:
- `-b N` → Define o tamanho `N` do setor do disco (válidos: 512, 1024, 2048, 4096 bytes).
- `-c [modo]` → Define o modo de compatibilidade com DOS (`dos` ou `nondos`).
- `-C [N]` → Especifica o número `N` de cilindros do disco (pouco comum de se usar).
- `-h` → Mostra a ajuda do comando `fdisk`.
- `-H` → Define o número de cabeças do disco, afetando a organização da tabela de partição.
- `-l` → Lista as tabelas de partição dos dispositivos conectados.
- `-S` → Especifica o número de setores por faixa (comum em 63).
- `-u [unidade]` → Mostra os tamanhos em setores ou cilindros.
- `-v` → Exibe a versão do `fdisk`.

Na interface:
- `b` → Especifique o tamanho do setor do disco. Os valores válidos são 512 , 1024 , 2048 ou 4096 . Os kernels recentes sabem o tamanho do setor. Use isso apenas em kernels antigos ou para substituir as ideias do kernel.
- `d` → Exclui uma partição.
- `F` → Lista partições não particionadas livres.
- `l` → Lista os tipos de partições conhecidas.
- `n` → Adiciona uma nova partição.
- `p` → Mostra a tabela de partição.
- `t` → Altera o tipo da partição.
- `v` → Verifica a tabela de partição.
- `i` → Mostra informação sobre uma partição.
- `m` → Mostra este menu.
- `u` → Altera as unidades das entradas mostradas.
- `x` → Funcionalidade adicional (somente para usuários avançados).
- `I` → Carrega layout de disco de um arquivo script de `sfdisk`.
- `O` → Despeja layout de disco para um arquivo script de `sfdisk`. 
- `w` → Grava a tabela no disco e sai.
- `q` → Sai sem salvar as alterações.
- `g` → Cria uma nova tabela de partição GPT vazia.
- `G` → Cria uma nova tabela de partição SGI (IRIX) vazia.
- `o` → Cria uma nova tabela de partição DOS vazia.
- `s` → Cria uma nova tabela de partição Sun vazia.

### Sintaxe comum:
**`# fdisk [OPÇÕES] PARTIÇÃO`**

### Exemplos:
`$ sudo fdisk -l`  → Mostra as partições do sistema.

`# fdisk /dev/loop20` → Acessa o menu interativo do dispositivo `/dev/loop20`.

`# fdisk -s /dev/sda1` → Visualiza as informações, como tamanho em blocos, da partição `/dev/sda1`.

### Máterial Complementar:
https://www.certificacaolinux.com.br/comando-linux-fdisk/

---

## `free`

### Para que serve?
O comando `free` no Linux é utilizado para **exibir informações sobre o uso de memória no sistema**, incluindo a memória física (RAM) e a memória de swap. Esse comando fornece detalhes importantes sobre a quantidade total, usada, livre e disponível de memória e swap.

#### Informações Retornadas pelo `free`
- **total:** Quantidade total de memória.
- **used:** Memória em uso.
- **free:** Memória atualmente livre.
- **shared:** Memória compartilhada entre processos.
- **buff/cache:** Memória em buffer e cache que pode ser liberada se necessário.
- **available:** Memória disponível para uso imediato por novos processos.

### Opções:
- `-b` → Exibe a memória em bytes.
- `-m` → Exibe a memória em megabytes.
- `-g` → Exibe a memória em gigabytes.
- `-h` → Exibe a memória em formato legível para humanos (automaticamente ajustando para KB, MB, ou GB).
- `-s [N]` → Atualiza a exibição a cada `N` segundos, útil para monitoramento em tempo real.
- `-t` → Adiciona uma linha com o total geral de memória (RAM + swap).

### Sintaxe comum:
**`free [OPÇÕES]`**

### Exemplos:
`$ free -m` → Mostra a quantidade de memória RAM utilizada em megabytes.

`$ free -h` → Mostra a quantidade de memória RAM utilizada em formato mais legível para humanos.

`$ free -t` → Mostra o total de memória utilizada.

`$ free -s 5` → Mostra os dados comuns do `free` atualizando a cada 5 segundos.

`$ free -hts 3` → Mostra os dados de forma mais legível para humanos, juntamente com o total de memória, atualizando a cada 3 segundos.

---

## `history`

### Para que serve?
Utilizado para **mostrar o histórico de comandos dados no Shell.**

Local onde armazena os comandos executados `.bash_history`.
O arquivo `.bashrc` diz quantos comandos é possível salvar.

Comandos com ` ` antes do comando não ficam salvos no histórico.

### Opções:
- `-d [N]` → Apaga o comando de número `N`.
- `!N` → Executa o comando de número `N`.
- `!!` → Executa o ultimo comando executado.
- `!?string?` → Executa o ultimo comando que equivale com a `string`.

- Ctrl + r → Procura pelo comando utilizando caracteres.

### Sintaxe comum:
**`$ history NÚMERO`**

### Exemplos:
`$ history` → Mostra todos os comandos.

`$ history 10` → Mostra os últimos 10 comandos executados.

`$ history -d 1200` → Apaga o comando de número 1200 e salva outro no lugar.

`$ !1293` → Executa o comando número 1293.

`$ !?dat?` → Executa o ultimo comando que tem o nome semelhante a `dat`.

---

## `iostat`

### Para que serve?


### Opções:
- `opção` →

### Sintaxe comum:
**`Sintaxe`**

### Exemplos:
`Exemplo 1` →

`Exemplo 2` →

### Máterial Complementar:
https://link;comum.com.br/

---

## `nice`

### Para que serve?
O comando `nice` é usado para iniciar processos com uma prioridade ajustada de CPU. A prioridade, chamada "nível de *nice*", determina a "gentileza" do processo com relação ao uso do processador, onde valores maiores tornam o processo "menos prioritário" (executado depois de processos de menor valor de *nice*). 

### Opções:
- `-n PRIORIDADE` → Define o nível de *nice* do processo que será iniciado. Se não especificado, o valor padrão é **10**.
- `--adjustment=[N]` → Mesma função que `-n`, define o valor de nice com o valor `N`.

### Sintaxe comum:
**`$ nice [OPÇÕES] COMANDO [ARGUMENTOS]`**

### Exemplos:
`$ nice -n 10 sleep 100` → Inicia o processo `sleep 100` com nível de *nice* 10.

`$ nice -10 rm -f arquivos.txt` → Inicia o processo `rm -f` com nível de prioridade -10.

`$ sudo nice -n -5 make` → Inicia o processo `make` com nível de *nice* -5, concedendo-lhe maior prioridade de CPU.

`$ ps -o pid,nice,cmd -p <PID>` → Verifica o nível de prioridade de um processo em execução.

### Máterial Complementar:
[https://link;comum.com.br/](https://www.certificacaolinux.com.br/comando-linux-nice/)

---

## `ionice`

### Para que serve?
O comando `ionice` é usado para **ajustar a prioridade de entrada/saída (I/O) de processos no sistema.** Isso permite que um administrador defina como um processo interage com o disco, ajustando sua prioridade de leitura e escrita. 

Diferentemente de comandos como `nice` ou `renice`, que ajustam a prioridade de uso da CPU, o `ionice` controla a prioridade de acesso ao disco. Isso é útil para evitar que processos intensivos em I/O interfiram negativamente em outros processos no sistema.

#### Classes de Agendamento I/O:
O `ionice` utiliza três classes principais de agendamento:
1. **Idle (Classe 3):**
    - O processo só usará o disco se ele não estiver ocupado por outro processo.
    - Ideal para tarefas que não são críticas, como backups ou verificações de disco.
2. **Best Effort (Classe 2 - padrão):**
    - Os processos recebem prioridade baseada em um nível de 0 a 7 (0 é a mais alta prioridade e 7 a mais baixa).
    - Se nenhuma prioridade for especificada, o padrão do kernel será usado.
3. **Realtime (Classe 1):**
    - Processos com acesso imediato ao disco.
    - Deve ser usado com cautela, pois pode monopolizar o I/O e afetar o desempenho de outros processos.

### Opções:
- `-cN` ou `--class [N]` → Define a classe de agendamento I/O (1 para **realtime**, 2 para **best-effort**, 3 para **idle**).
- `-nN` ou `--classdata [N]` → Define a prioridade dentro da classe **best-effort** (0 a 7, onde 0 é a mais alta prioridade).
- `-pPID` ou `--pid PID` → Altera a prioridade I/O de um processo já em execução, especificado pelo PID.
- -`t` ou `--ignore` → Ignora erros e continua mesmo que o processo não seja alterável.
- `-h` ou `--help` → Exibe a ajuda do comando e sai.

### Sintaxe comum:
**`$ ionice [OPÇÕES] [COMANDO]`**
**`$ ionice [OPÇÕES] -p PID`**

### Exemplos:
`$ ionice -c3 rsync -av /origem /destino` → O comando `rsync` será executado com prioridade idle, só usando o disco quando ele estiver ocioso.

`# ionice -c2 -n5 -p 1234` → Ajusta o processo com PID `1234` para a classe **best-effort** com prioridade média (nível 5).

`$ ionice -c1 dd if=/dev/zero of=/tmp/test.img bs=1M count=100` → O comando dd será executado com prioridade máxima, garantindo acesso imediato ao disco.

`$ ionice -c2 -n7 tar -czf backup.tar.gz /meu/diretorio` → O comando tar será executado com baixa prioridade, reduzindo o impacto em outros processos.

`$ ionice -p PID` → Para verificar a prioridade I/O de um processo em execução.

### Máterial Complementar:
https://www.geeksforgeeks.org/ionice-command-in-linux-with-examples/

---

## `top`

### Para que serve?
Utilizado para **monitorar em tempo real o desempenho do sistema e exibir uma lista dos processos em execução**, mostrando informações detalhadas como:
- **Uso de CPU** → Exibe a porcentagem de uso da CPU pelo sistema e pelos processos.
- **Uso de memória** → Mostra quanto da memória física (RAM) está sendo usada e quanto está disponível.
- **Processos ativos** → Exibe uma lista dos processos em execução no sistema, ordenados pelo uso de CPU (por padrão).
- **Informações do sistema** → Informações gerais sobre a carga do sistema, como o tempo de atividade (uptime), carga média (load average), e o número de processos. 

Ele é uma ferramenta interativa que permite ver rapidamente o que está acontecendo no sistema e pode ser usado para identificar processos que estão consumindo muitos recursos.

**PID** → é o ID do processo que você deseja atingir. Para obter o PID de um processo, você pode usar o comando `ps`, `top`, ou `pgrep`.

### Opções:
- `-d N` → define o intervalo de atualização em N segundos do top (padrão é 3 segundos)
- `-p <PID>` → define qual processo vai ser monitorado com base no PID
- `-u  USER` → define quais processos vão ser mostrados com base no nome do usuário

#### Comandos dentro do `top`:
- `h` → Exibe a ajuda do top com uma lista completa de comandos interativos.
- `k` → Enviar um sinal de término (kill) a um processo. Você será solicitado a fornecer o PID e o sinal.
- `M` → Ordena a lista de processos pelo uso de memória.
- `P` → Ordena a lista de processos pelo uso de CPU (padrão).
- `q` → Sai do top e volta para o terminal.
- `r` → Renomear um processo (muda a prioridade/niceness).
- `z` → Ativa ou desativa o modo de cores para destacar o uso de CPU e memória.

### Sintaxe comum:
**`$ top [OPÇÕES]`**

### Exemplos:
`$ top` → Mostra as informações em tempo real os processos em execução.

`$ top -d 2` → Define um intervalo de 2 segundos de atualização do top.

`$ top -p 10833` → Mostra os detalhes de somente o processo com PID 10833.

`$ top -u root` → Mostra somente os processos do usuário root.

### Máterial Complementar:
https://learn.microsoft.com/pt-br/troubleshoot/developer/webapps/aspnetcore/practice-troubleshoot-linux/3-2-task-managers-top-htop

---

## `htop`

### Para que serve?
O comando `htop` é um visualizador de processo e um aplicativo de modo de texto para **monitoramento do sistema em tempo real**, semelhante a `top`. É fácil de usar e exibe uma lista completa dos processos em execução.

### Comandos dentro do htop:
- `H` → Desabilita a exibição de thread (para tornar a saída mais clara).
- `U` → Seleciona o nome de usuário em uma lista para mostrar os processos dele.
- `f9` → Utilizado para mandar mensagem par ao comando selecionado.
- `f10` → Sai do `htop`.

### Máterial Complementar:
<img src="https://github.com/pedcravo/Wiki/blob/main/Linux/htop1.webp" width="600px">

<img src="https://github.com/pedcravo/Wiki/blob/main/Linux/htop2.png" width="600px">

https://blog.ironlinux.com.br/o-comando-htop-no-linux/

https://blog.ironlinux.com.br/o-comando-htop-no-linux/

---

##

### Para que serve?


### Opções:
- `opção` →

### Sintaxe comum:
**`Sintaxe`**

### Exemplos:
`Exemplo 1` →

`Exemplo 2` →

### Máterial Complementar:
https://link;comum.com.br/

---