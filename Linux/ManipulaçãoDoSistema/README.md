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
11. [`vmstat`]()
12. [`jobs`](#jobs)
13. [`kill`](#kill)
14. [`modprobe`](#modprobe)
15. [`mount` e `unmount`](#mount-e-unmount)
16. [`nice`](#nice)
17. [`ionice`](#ionice)
18. [`renice`](#renice)
19. [`pgrep`](#pgrep)
20. [`ps`](#ps)
21. [`pstree`](#pstree)
22. [`swapon`](#swapon)
23. [`systemctl`](#systemctl)
24. [`tmux`](#tmux)
25. [`top`](#top)
26. [`htop`](#htop)
27. [`tty`]()
28. [`tzselect`]()
29. [`uname`]()
30. [`uptime`]()

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
O comando `iostat` é usado para **mostrar o relatório de uso de CPU e de entrada/saída dos dispositivos de armazenamento**, pode rodar em intervalos de tempo ou mostrar somente uma vez. Para ter informações completas é necessário utilizar o usuário `root`.

Ele pertence ao pacote `sysstat` e precisa ser instalado pois por padrão não vem no sistema. Esse pacote contém ferramentas para monitorar o uso e performance do sistema, que podem ser utilizadas diretamente ou agendadas para gerar relatórios.

#### Informações de saída:
1. **Sessão avg-cpu** → É o relatório referente à utilização do CPU desde o boot do sistema.
  - `%user`: percentual de uso da CPU durante a execução no nível de usuário (programas).
  - `%nice`: percentual de uso da CPU durante a execução no nível de usuário com prioridade alterada.
  - `%system`: esse dado é de nível de sistema (kernel).
  - `%iowait`: mostra a porcentagem de tempo em que a CPU estava ociosa, aguardando alguma resposta de escrita/leitura em disco.
  - `%steal`: é para uso em máquinas virtuais, tempo em que a CPU da máquina virtual ficou aguardando a CPU da máquina real.
  - `%idle`: tempo em que a CPU estava ociosa e não aguardava por entrada/saída de disco.
2. **Sessão device** → É utilização dos dispositivos de armazenamento do equipamento.- device: nome do dispositivo ou partição.
  - `tps`: transferências por segundos feitas no dispositivo.
  - `kB_read/s` e `kB_wrtn/s`: quantidade de dados lidos e gravados no dispositivo.
  - `kB_read` e `kB_wrtn`: quantidade de dados lidos e gravados no dispositivo no intervalo.

### Opções:
- `-c` → Mostra apenas a CPU.
- `-d` → Mostra os devices.
- `-h` → Mostra os dados em formato de melhor leitura para humanos.
- `-m` → Mostra os dados em forma de megabytes.
- `-p` → Mostra os dados das partições.

### Sintaxe comum:
**`# iostat [OPÇÕES] SEGUNDOS`**

### Exemplos:
`# iostat -h 2` → Mostra relatório em um formato de melhor leitura em um intervalo de 2 segundos.

`# yum install sysstat` → Utilizado para instalar o pacote de comandos sysstat.

### Máterial Complementar:
https://www.site24x7.com/pt/learn/linux/troubleshoot-high-io-wait.html

https://amaurybsouza.medium.com/capacityplanning-8991ddb3bef3

---

## `vmstat`

### Para que serve?
O comando `vmstat` é utilizado para **exibir estatísticas detalhadas do sistema, monitorando recursos como CPU, memória, e atividades de disco.** Ele permite analisar o desempenho do sistema em tempo real e ajuda a identificar possíveis gargalos.

#### Principais Colunas do vmstat
1. **Procs**: Informações sobre processos.
     - **r** → Número de processos em espera para execução (fila de execução).
     - **b** → Número de processos bloqueados e esperando por E/S.
2. **Memory**: Dados sobre o uso de memória.
     - **swpd** → Quantidade de memória em swap (em KB).
     - **free** → Quantidade de memória RAM livre (em KB).
     - **buff** → Memória em buffer (armazenamento temporário).
     - **cache** → Memória em cache (armazenamento temporário de arquivos e dados).
3. **Swap**: Estatísticas de swap.
     - **si** → Quantidade de memória movida do disco (swap) para a RAM por segundo.
     - **so** → Quantidade de memória movida da RAM para o disco (swap) por segundo.
4. **IO**: Atividades de entrada e saída de dados.
     - **bi** → Taxa de dados lidos (em blocos) por segundo.
     - **bo** → Taxa de dados gravados (em blocos) por segundo.
5. **System**: Informações sobre interrupções e chamadas ao sistema.
     - **in** → Número de interrupções por segundo.
     - **cs** → Número de trocas de contexto por segundo (muda um processo ativo para outro).
6. **CPU**: Estatísticas de uso da CPU.
     - **us** → Tempo que a CPU passa em modo usuário (em %).
     - **sy** → Tempo que a CPU passa em modo sistema (em %).
     - **id** → Tempo em que a CPU permanece ociosa (em %).
     - **wa** → Tempo que a CPU passa esperando operações de E/S (em %).
     - **st** → Tempo roubado da CPU pela máquina virtual (em %), em ambientes virtualizados.

#### Observações:
- **CPU alta em `wa`**: Uma porcentagem alta em `wa` indica que a CPU está frequentemente esperando por operações de E/S, um possível indicador de gargalo de disco.
- **CPU ociosa (`id`)**: Uma alta porcentagem de `id` geralmente indica que a CPU está aguardando tarefas, o que pode ser normal em sistemas de baixa carga.

### Opções:
- `-a` → Inclui estatísticas de memória ativa e inativa.
- `-d` → Exibe estatísticas de disco.
- `-f` → Exibe o número total de forks (processos criados) desde o início do sistema.
- `-s` → Exibe um resumo de estatísticas do sistema desde o início do sistema.
- `-t` → Adiciona a data e hora a cada linha da saída.

### Sintaxe comum:
**`vmstat [OPÇÕES] [SEGUNDOS] [REPETIÇÕES]`**

### Exemplos:
`$ vmstat` → Mostra a lista na tela. 

`$ vmstat 2` → Mostra e atualiza a cada 2 segundos a lista de processos. 

`$ vmstat 2 5` → Atualiza 5 vezes a tabela a cada 2 segundos,

`$ vmstat -d` → Exibe informações detalhadas sobre o uso do disco.

`$ vmstat -t 1 3` → Exibe estatísticas a cada segundo, três vezes, incluindo a data e a hora.

### Máterial Complementar:
https://amaurybsouza.medium.com/capacityplanning-8991ddb3bef3

---

## `jobs`

### Para que serve?
O comando `jobs` é utilizado para **listar e gerenciar processos em execução ou suspensos no terminal atual**, ele mostra o status de tarefas em segundo plano e suspensas.

Ele ajuda a monitorar tarefas que foram iniciadas pelo terminal e que estão rodando ou aguardando para serem retomadas.

#### Informações exibidas pelo `jobs`:
```bash
[1]+  Parado                  top
[2]   Parado                  top
[3]-  Parado                  top
```

- **Número da Tarefa** `[1]` → Indicado por `%n` (ex: `%1`, `%2`).
- **Símbolo**  `+` / `-` → Indica a tarefa **principal** e a **secundária**, respectivamente.
- **Status da Tarefa** → Mostra se o processo está *Running* (executando), *Stopped* (parado ou suspenso), *Terminated* (terminado).
- **Comando** → O comando que iniciou a tarefa.

#### Comandos relacionados:
- `bg` → Retoma uma tarefa em segundo plano.
- `fg` → Traz uma tarefa para o primeiro plano.

### Opções:
- `-l` → Exibe o ID do processo (PID) de cada tarefa junto com o status.
- `-p` → Exibe apenas o PID das tarefas.
- `-r` → Mostra apenas as tarefas em execução.
- `-s` → Mostra apenas as tarefas suspensas.

### Sintaxe comum:
**`$ jobs [OPÇÕES]`**

### Exemplos:
`$ jobs` → Lista todas as tarefas em segundo plano e suspensas no terminal atual.

`$ jobs -l` → Lista todas as tarefas com o PID de cada uma.

`$ jobs -r` → Mostra apenas as tarefas que estão em execução.

`$ jobs -s` → Exibe apenas as tarefas que estão suspensas.

---

## `kill`

### Para que serve?
**Utilizado para enviar sinais a processos, permitindo que você controle ou interrompa a execução de processos em execução no sistema.**

Ele é amplamente utilizado para **terminar processos**, mas também pode enviar outros tipos de sinais além de encerrar um processo, como pausar, continuar ou reiniciar um processo.

> Por padrão `kill` envia sinal **15** (`SIGTERM`), sinal para encerrar o processo.

O `kill` faz uso do PID para identificar e finalizar o comando.
O PID é o ID do processo que você deseja atingir. Para obter o PID de um processo, você pode usar o comando `ps`, `top`, ou `pgrep`.

### Opções:
- `-1` ou `SIGHUP` → Sinal para reiniciar processo.
- `-9` ou `SIGKILL` → Sinal para forçar encerramento imediato do processo.
- `-15` ou `SIGTERM` → Sinal para encerrar o processo de maneira controlada (sinal padrão).
- `-18` ou `SIGCONT` → Continua o processo pausado pelo 19.
- `-19` ou `SIGSTOP` → Pausa a execução do processo.

#### Variantes do `kill`
- `killall` → Encerra todos os processos de mesmo nome.
- `pkill` → Encerra processos utilizando o nome como base.

### Sintaxe comum:
**`$ kill [OPÇÕES] <PID>`**

**`$ killall NOME_DO_PROCESSO`**

**`$ pkill NOME_DO_PROCESSO`**

### Exemplos:
`$ kill 6978` → Para e fecha o programa de PID `6978` usando sinal padrão.

`$ kill -9 15400` → Força fechada imediata do processo de PID `15400`.

`$ kill -19 15400`  or `$ kill -STOP 15400` → Pausa processo.

`$ kill -18 15400` or `$ kill -CONT 15400`  → Continua processo antes pausado.

`$ kill %2` → Finaliza o processo de número 2 dos processos em segundo plano.

`$ kill -9 %2` → Força a finalização do processo de número 1 dos processos em segundo plano.

#### `killall`
`$ killall firefox` → Encerra todos os processos de nome firefox.

#### `pkill`
`$ pkill firefox` → Encerra o processo com o nome firefox.

### Máterial Complementar:
https://ryanstutorials.net/linuxtutorial/processes.php

---

## `modprobe`

### Para que serve?
O comando `modprobe` é usado para **gerenciar módulos do kernel no Linux, permitindo carregar, descarregar ou listar módulos de forma dinâmica.** Um módulo é uma extensão do kernel que pode ser carregada em tempo de execução, como drivers de hardware.

- O modprobe carrega automaticamente módulos dependentes ao carregar um módulo principal.
- Ele é comumente usado em conjunto com outros comandos relacionados, como `lsmod` (para listar módulos carregados) e `rmmod` (para remover módulos).

> **OBS:**
> O comando trabalha diretamente com os módulos armazenados em `/lib/modules/$(uname -r)`.

### Opções:
- `-a` → Carrega múltiplos módulos ao mesmo tempo.
- `-r` → Remove um módulo do kernel (similar ao `rmmod`).
- `--show-depends` → Exibe os módulos dependentes que serão carregados junto com o módulo especificado.
- `-v` → Ativa o modo verboso, exibindo mais informações sobre as ações realizadas.
- `--dry-run` → Simula o carregamento do módulo sem realmente executá-lo.
- `--force` → Força o carregamento do módulo, mesmo que seja incompatível com a versão do kernel.
- `--first-time` → Carrega o módulo apenas se ele ainda não foi carregado.

### Sintaxe comum:
**`$ modprobe [OPÇÕES] MÓDULO`**

### Exemplos:
`$ sudo modprobe parport` → Carrega o módulo `parport` no kernel, usado para compartilhar portas paralelas.

`$ sudo modprobe -r parport` → Remove o módulo `parport` do kernel.

`$ modprobe --show-depends parport` → Mostra os módulos que serão carregados como dependências ao carregar o módulo `parport`.

`$ modprobe --dry-run parport` → Simula o carregamento do módulo `parport` sem efetivamente carregá-lo.

`$ sudo modprobe -a parport lp` → Carrega os módulos `parport` e `lp` (impressora paralela) simultaneamente.

`$ sudo modprobe --force modulo_teste` → Força o carregamento do módulo `modulo_teste`, mesmo que ele seja incompatível com o kernel atual.

`$ sudo modprobe -v parport` → Carrega o módulo `parport` e exibe informações detalhadas sobre o processo de carregamento.

---

## `mount` e `unmount`

### Para que serve?
O comando `mount` é usado para **montar dispositivos e sistemas de arquivos na hierarquia do sistema Linux, tornando-os acessíveis no sistema de arquivos.** A montagem é feita em um "ponto de montagem", que é normalmente um diretório vazio.

Já o comando `umount` é a contraparte de `mount` e é utilizado para **desmontar dispositivos, sincronizar e liberar o ponto de montagem.**

O sistema de arquivos Linux (FHS) define pontos de montagem como `/mnt` para uso temporário e `/media` para mídias removíveis. Outras pastas também podem ser usadas como ponto de montagem, desde que estejam vazias.

O sistema de arquivos do Linux é hierárquico e admite que diversos dispositivos sejam mapeados e utilizados a partir da raiz do sistema `/` (`root`).

#### Arquivos relacionados
- `/etc/fstab` → Lista as configurações de montagem para dispositivos. Ao usar `mount -a`, todos os dispositivos neste arquivo são montados.
- `/etc/mtab` → Mantém um registro dos dispositivos atualmente montados, atualizado pelo `mount`.
- `/proc/mounts` → Outra fonte de informações sobre dispositivos montados, mantida pelo kernel.
- `/proc/partitions` → Lista discos e partições detectados.

### Mount

#### Opções:
- `-a` → Monta todos os dispositivos configurados no `/etc/fstab` (exceto aqueles com a opção `noauto`).
- `-r` → Monta o sistema de arquivos em modo somente leitura.
- `-w` → Monta o sistema de arquivos com permissão de leitura e gravação.
- `-o` → Define opções de montagem, como noatime, sync, entre outras.
- `-t [TIPO]` → Especifica o `TIPO` de sistema de arquivos (por exemplo, `ext4`, `vfat`, `iso9660`, etc.).
- `-o loop` → Monta arquivos de imagem, como `.iso`, usando um loopback.

#### Sintaxe comum:
**`$ mount [OPÇÕES] DISPOSITIVO/DIRETORIO`**

#### Exemplos:
`# mount /dev/sdb1 /mnt` → Monta um dispositivo USB em `/mnt`.

`# mount -t vfat -o ro /dev/sda1 /mnt` → Monta uma partição vfat como somente leitura.

`# mount -o remount,ro /` → Remonta a partição raiz como somente leitura.

`# mount -o loop /tmp/imagem.iso /media/iso` → Monta uma imagem ISO usando `loop`.

`# mount UUID="1c3b15b1-cd13-4a73-b2a8-449fa3aa039f" /mnt` → Montar um dispositivo usando o `UUID`.

### Unmount

#### Opções:
- `-a` → Desmonta todos os dispositivos listados em `/etc/mtab`.
- `-f` → Força a desmontagem, útil em sistemas remotos que não estão respondendo.
- `-t [TIPO]` → Desmonta apenas dispositivos de um `TIPO` específico de sistema de arquivos.

#### Sintaxe comum:
**`$ unmount [OPÇÕES] DISPOSITIVO/DIRETORIO`**

#### Exemplos:
`# umount /media/usb` → Desmonta um dispositivo a partir do diretório.

`# umount /dev/sdb1` → Desmonta um dispositivo pelo nome.

`# umount -a` → Desmonta todos os sistemas de arquivos listados em `/etc/mtab`.

### Máterial Complementar:
https://www.certificacaolinux.com.br/comando-linux-mount/

---

## `nice`

### Para que serve?
O comando `nice` é usado para **iniciar processos com uma prioridade ajustada de CPU**. A prioridade, chamada "nível de *nice*", determina a "gentileza" do processo com relação ao uso do processador, onde valores maiores tornam o processo "menos prioritário" (executado depois de processos de menor valor de *nice*). 

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

## `renice`

### Para que serve?
O comando `renice` é utilizado para **ajustar a prioridade de execução de processos em execução, alterando seu valor de prioridade.** Esse comando permite que você ajuste quais processos terão mais ou menos acesso aos recursos do sistema, sendo útil para gerenciar cargas de trabalho em servidores e sistemas com vários processos ativos.

• **Prioridade:** O ajuste de prioridade é um número inteiro de **-20** (alta prioridade) até **+19** (baixa prioridade).
• **Permissões:** Usuários comuns podem **diminuir a prioridade** de seus próprios processos, mas apenas o `root` pode aumentar a prioridade.

### Opções:
- `-g` → Ajusta a prioridade de todos os processos de um grupo específico.
- `-n` → Define o valor incremento de prioridade (é opcional pois faz o mesmo que o comando padrão).
- `-p` → Especifica o PID do processo para o qual a prioridade será ajustada.
- `-u` → Ajusta a prioridade de todos os processos de um usuário específico.

### Sintaxe comum:
**`$ renice PRIORIDADE [OPÇÕES] PROCESSO`**

### Exemplos:
`$ renice +2 30018` → Altera a prioridade do processo `30018` de **0** para **+2**.

`$ sudo renice 0 30018` → Volta com a prioridade **0** para o processo `30018`.

`$ renice +5 -u daemon` → Ajusta a prioridade de todos os processos pertencentes ao usuário `daemon` para **+5**.

`$ renice -n +5 -p 12345` → Muda a prioridade do processo `12345`, adiciona **+5** a prioridade atual do processo.

`$ renice -5 -g grupo` → Aumenta a prioridade de todos os processos do grupo `grupo` para **-5**.

`# renice -1 987 -u daemon root -p 32` → Altera a prioridade dos processos com PID `987` e `32`, bem como todos os processos dos usuários `daemon` e `root`.

### Máterial Complementar:
https://www.certificacaolinux.com.br/comando-linux-nice/

---

## `pgrep`

### Para que serve?
O comando `pgrep`, ou *Process Grep*, é utilizado para **procurar por processos atualmente em execução no sistema, com base em um nome de processo completo ou parcial ou em outros atributos especificados.** Ele é uma derivação do comando `grep` juntamente com o comando `ps`.

### Opções:
- `-c` → Mostra somente a contagem de processos correspondentes.
- `-d` → Define qual delimitador vai ser usado para separar cada PID, o padrão é a quebra de linha. 
- `-f` → Procura pelo padrão na linha inteira, não somente no nome.
- `-l` → Mostra o nome do processo juntamente com o PID.
- `-n` → Seleciona apenas o processo mais recente.
- `-u` →  Seleciona o usuário, pesquisa os processos relacionados a ele.

### Sintaxe comum:
**`$ pgrep [OPÇÕES] PADRÃO`**

### Exemplos:
`# pgrep ssh` → Procura pelos processos com o padrão `ssh`.

`# pgrep -u root ssh` → Procuram pelos processos do usuário root que tem o padrão `ssh`.

`# pgrep -l ssh` → Mostra o nome do processo com padrão `ssh` juntamente com seu o PID.

`# pgrep -lnu root` → Procura pelo processo mais recente do usuário `root`.

`# pgrep ssh -d' '` → Mostra todos os PID dos processos com padrão `ssh` em sequencia utilizando ` ` entre eles.

`# pgrep -f zen` → Procura pelo padrão zen por toda a linha dos processos, não apenas no nome deles, mostrando apenas o PID dos processos encontrados. 

### Máterial Complementar:
https://www.certificacaolinux.com.br/comando-linux-pgrep/

https://www.linuxforce.com.br/comandos-linux/comandos-linux-comando-pgrep/

---

## `ps`

### Para que serve?
Utilizado para **exibir informações sobre processos em execução no sistema.**
(Process Status)

### Opções:
- `a` → Lista todos os processos associados a um terminal executados atualmente.
- `-a` - Lista processos associados a um terminal, excluindo líderes de sessão.
- `-e` → Exibe todos os processos ativos no sistema.
- `f` → Mostra os processos atuais do sistema associados ao terminal, mostra em forma de árvore.
- `-f` → Mostra informações detalhadas dos processos.
- `u` → Exibe todos os processos sendo executados no usuário atual, em primeiro plano.
- `-u` → Lista processos de um usuário específico.
- `x` → Mostra processos sem terminal (como serviços em segundo plano) sendo executados atualmente.

#### Junção de opções:
- `ax` → `a` + `x` → Mostra os processos já executados, anteriormente e agora.
- `au` → `a` + `u` → Mostra todos os processos realizados pelo usuário atual em um terminal.
- `ux` → `u` + `x` → Mostra todos os processos executados do usuário atual, inclusive os processos em segundo plano.
- `aux` → Mostra todos os processos já executados no sistema, pelo usuário atual e outros.
- `fax` → Mostra o mesmo que ax porém com uma árvore indicando comandos pais e filhos.

### Sintaxe comum:
**`$ ps [OPÇÕES]`**

### Exemplos:
`$ ps` → Lista processos do terminal atual.

`$ ps aux` → Lista todos os processos, com informações detalhadas (junção dos comandos a, u e x).

`$ ps aux | less` → Lista de forma detalhada as informações por intermédio do less (usa interface do less).

`$ ps aux | head` → Mostra os 10 maiores processos.

`$ ps -ef` → Mostra os processos com caminho absoluto.

`$ ps -ef | grep apache` → Procura processos relacionados ao "apache”.

`$ ps -u pedrocravo` → Lista processos do usuário "pedrocravo".

`$ ps fax` → Mostra os comandos pais e filhos.

---

## `pstree`

### Para que serve?
O comando `pstree` **exibe os processos ativos no sistema em formato de árvore hierárquica, mostrando relações de origem e descendência entre processos (como processos "pai" e "filho").** Ele é útil para visualizar como os processos são organizados e hierarquizados no sistema.

Ele mostra os porcessos em **bg** bem como aqueles em **fg**.

### Opções:
- `-a` → Exibe detalhes completos de cada processo, incluindo argumentos da linha de comando.
- `-c` → Não agrupa processos com o mesmo nome em uma única linha (por padrão, processos com o mesmo nome podem ser agrupados).
- `-h` → Destaca o processo atual (útil para localizar processos relacionados ao shell atual).
- `-l` → Mostra uma lista completa em uma única linha, sem truncar (melhor para exibir em terminais largos).
- `-n` → Organiza os processos na ordem de PID.
- `-p` → Exibe os PIDs (IDs dos processos) ao lado dos nomes dos processos.
- `-s` → Exibe apenas a linha de hierarquia que leva a um processo específico, especificado por PID.

### Sintaxe comum:
**`pstree [OPÇÕES] <USUÁRIO|PID>`**

### Exemplos:
`$ pstree -a` → Mostra argumentos completos dos processos.

`$ pstree -np` → Mostra os processos, cada um com seus PID, ordenados em ordem crescente de PID.

`$ pstree -s 12839` → Mostra o caminho de somente o processo de PID `12839`.

`$ pstree pedro` →  Mostra todos os processos inicializados pelo usuário pedro.

---

## `swapon`

### Para que serve?
O comando `swapon` é utilizado para **ativar e gerenciar partições ou arquivos de swap no Linux.**

**Swap** é uma área no disco rígido usada pelo sistema como uma extensão de memória RAM, útil quando a RAM física é insuficiente para manter todos os processos.

> Desativar o swap pode ser feito com o comando `swapoff`.

#### Arquivos relacionados:
- `/etc/fstab`→ Arquivo de configuração onde estão listados dispositivos e arquivos de swap que devem ser ativados automaticamente.
- `/proc/swaps`→ Arquivo que mostra áreas de swap ativas e informações detalhadas.

#### Configuração:
Para que uma área de swap seja ativada automaticamente no **boot**, adicione uma linha para o dispositivo ou arquivo de swap no `/etc/fstab`. A linha geralmente segue o formato:
```bash
/dev/sdXn  swap  swap  defaults  0 0
```

ou, para arquivos de swap:
``` bash
/swapfile  none  swap  sw  0 0
```

### Opções:
- `-a` → Ativa todas as partições e arquivos de swap listados em `/etc/fstab`.
- `-d` → Desativa uma área de swap específica (requer nome ou dispositivo como argumento).
- `-e` → Ignora dispositivos de swap que não são válidos (ao usar com `-a`).
- `-f` → Força a ativação do swap, mesmo que haja erros ou inconsistências.
- `-p [N]` → Define a prioridade do dispositivo ou arquivo de swap, onde maiores números têm maior prioridade (útil quando há várias áreas de swap).
- `-s` ou `--show` → Exibe uma lista de todas as áreas de swap ativas.

### Sintaxe comum:
**`swapon [OPÇÕES] [DISPOSITIVO/ARQUIVO]`**

### Exemplos:
`$ swapon -a` → Ativa todas as partições de swap listadas em `/etc/fstab`.

`$ swapon /dev/sda2` → Ativa a partição `/dev/sda2` como área de swap.

`$ swapon -p 5 /swapfile` → Define prioridade para uma partição específica de swap.

`$ swapon -s` → Mostra a partição do disco sendo utilizada como memória swap.

---

## `systemctl`

### Para que serve?
O `systemctl` é o comando principal do pacote **systemd** **para gerenciar serviços e unidades (chamadas de "units") no Linux, abrangendo inicialização, parada, reinicialização, habilitação e monitoramento de serviços do sistema.**

O `systemctl` é usado para **controlar e visualizar o status de serviços, montagens, dispositivos, soquetes e outras unidades no sistema.** Ele é fundamental para gerenciar serviços do sistema em distribuições modernas, como Ubuntu, CentOS, e Fedora.

**Units** → Unidades de execução, podem executar um ou mais serviços.

#### Os principais tipos de Units:
- `.service` → Executa e controla um serviço.
- `.target` → Agrupa várias unidades para inicializar em conjunto, como `multi-user.target`.
- `.mount` → Monta um sistema de arquivos.
- `.timer` → Agenda a execução de uma unidade em intervalos específicos.

#### Caminho das Unidades
As unidades são geralmente encontradas em:
- `/etc/systemd/system/` → Configurações de unidades personalizadas pelo usuário.
- `/usr/lib/systemd/system/` → Configurações de unidades do sistema.

### Opções:
- `status` → Exibe o status de uma unidade, incluindo logs e informações sobre seu estado atual.
- `start` → Inicia uma unidade imediatamente.
- `stop` → Para uma unidade imediatamente.
- `restart` → Reinicia uma unidade, útil para aplicar configurações alteradas.
- `reload` → Recarrega a configuração de uma unidade sem reiniciá-la completamente, se o serviço suportar.
- `enable` → Configura uma unidade para iniciar automaticamente no boot.
- `disable` → Remove a configuração de inicialização automática da unidade.
- `list-units` → Lista todas as unidades ativas do sistema.
- `list-unit-files` → Exibe a lista de todas as unidades com seus status de habilitação.
- `is-active` → Verifica se uma unidade está ativa.
- `is-enabled` → Verifica se uma unidade está configurada para iniciar no boot.
- `mask` → Desabilita completamente uma unidade, impedindo sua ativação (direta ou indireta).
- `unmask` → Reverte a operação de mask, permitindo a ativação da unidade.

`/PROCESSO` → Procura pelo `PROCESSO` dentro da lista.

### Sintaxe comum:
**`$ systemctl [OPÇÃO] [UNIT]`**

### Exemplos:
`$ systemctl` → Mostra todos os serviços da máquina.

`$ systemctl start apache2` → Inicia o serviço `apache`.

`$ systemctl stop nginx` → Para o serviço `nginx`.

`$ systemctl status sshd` → Mostra o status do serviço SSH.

`$ systemctl restart network` → Reinicia o serviço de rede.

`$ systemctl enable firewalld` → Habilita o `firewall` para iniciar automaticamente.

`$ systemctl disable cups` → Desabilita o serviço de impressão `Cups` no boot.

`$ systemctl is-active docker` → Verifica se o serviço `Docker` está ativo.

`$ systemctl list-units --type=service` → Lista todas as unidades de serviço ativas.

`$ systemctl mask bluetooth` → Impede a ativação do serviço `Bluetooth`.

### Máterial Complementar:
https://www.digitalocean.com/community/tutorials/how-to-use-systemctl-to-manage-systemd-services-and-units-pt

https://www.certificacaolinux.com.br/comando-linux-systemctl/

https://youtu.be/CSqyL4aoNQc?si=RmBc-9WdXG4BjVBl

https://youtu.be/q4LU4MrucXo?si=aYJken-v2ShRwtta

---

## `tmux`

### Para que serve?
O `tmux` (Terminal Multiplexer) é uma ferramenta de **multiplexação de terminal que permite criar, gerenciar e alternar entre várias janelas de terminal em uma única sessão de terminal.** Ele é especialmente útil para:
- **Organizar múltiplos terminais** sem abrir várias janelas separadas.
- Deixar **processos rodando em segundo plano** mesmo após se desconectar do terminal (por exemplo, ao usar SSH).

Cada sessão do `tmux` pode conter várias janelas, e cada janela pode ser dividida em diversos painéis, permitindo uma organização eficiente do terminal.

### Opções:
- Ctrl + b + % → Divide a janela em duas abas horizontalmente.
- Ctrl + b + “ → Divide a janela em duas abas verticalmente.
- Ctrl + b + seta → Movimente a aba na direção indicada.
- Ctrl + d ou exit→ Fecha a aba.

### Sintaxe comum:
**`$ tmux [OPÇÕES]`**

### Exemplos:
`$ tmux` → Cria uma nove sessão.

`$ tmux new-session -s sessao` → Cria uma nove sessão com nome sessao.

`$ tmux attach-session -t 0` → Entra na sessão  0 do tmux.

`$ tmux ls` → Lista as sessões abertas.

`$ tmux switch -t 0`  → Alterna entre a sessões virtuais, sendo 0 o id da sessão destino.

`$ tmux kill-session -t 0` → Encerra sessão 0.

### Máterial Complementar:
https://www.certificacaolinux.com.br/comando-linux-tmux/

https://www.hostinger.com.br/tutoriais/como-usar-tmux-lista-de-comandos#Como_Instalar_o_Tmux

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

## `tty`

### Para que serve?
Utilizado para **exibir o nome do terminal associado à sessão atual**. (TeleTYpewriter)

O comando `tty` mostra o arquivo no qual o terminal (pseudo terminal) está aberto.

#### Saída padrão:
`/dev/pts/N` → Onde `N` varia de acordo com o número da tela aberta.

### Comandos semelhantes:
`$ ls /dev/pts` → Lista quais os terminais estão abertos.

`$ ls -1 /dev/pts | grep ‘[0-9]’`→ Lista quais os terminais estão abertos, organiza em coluna e mostra somente de 0 a 9.

`$ ls -1 /dev/pts | grep '[0-9]' > /dev/pts/1` → Lista quais os terminais estão abertos, organiza em coluna e mostra no terminal `/dev/pts/1` somente de 0 a 9.

---

## `tzselect`

### Para que serve?
O comando `tzselect` é usado para **configurar ou modificar o fuso horário do sistema Linux.** Ele orienta o usuário por meio de um assistente interativo, permitindo selecionar a região geográfica e o fuso horário correspondente.

Embora `tzselect` não aplique mudanças diretamente ao sistema, ele ajuda a determinar as configurações adequadas, que podem ser aplicadas manualmente posteriormente.

É semelhante ao comando `dpkg-reconfigure tzdata`, mas é mais genérico e disponível em várias distribuições Linux.

### Exemplos:
`$ tzselect` → Inicia o assistente interativo para escolher a localização geográfica e o fuso horário correspondente.

`# ln -sf /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime` → Após usar o `tzselect`, ele fornecerá o caminho do fuso horário selecionado, que pode ser aplicado ao sistema através deste comando.

---

## `uname`

### Para que serve?
Utilizado para **exibir informações sobre o sistema.** Por padrão, o `uname` exibe apenas o nome do kernel.

### Opções:
- `-a` → Mostra todas as informações disponíveis sobre o sistema: **nome do kernel, versão, nome da máquina, arquitetura**, etc.
- `-m` → Mostra qual arquitetura do computador (como `x86_64`, `arm`, etc.).
- `-n` → Mostra o nome do host (nome da máquina na rede).
- `-o` → Exibe o nome do sistema operacional.
- `-p` → Mostra o tipo de processador.
- `-r` → Mostra a versão do kernel do sistema.
- `-s` → Mostra somente o nome do kernel (**padrão**).
- `-v` → Mostra a versão do kernel com detalhes adicionais, incluindo o timestamp de compilação.

### Sintaxe comum:
**`$ uname [OPÇÕES]`**

### Exemplos:
`$ uname -a` → Mostra todas as informações disponíveis sobre o sistema.

`$ uname -mn` → Mostra o nome do qual o nome do host e arquitetura do computador.

`$ uname -op` → Mostra o tipo de processador juntamente com a o nome do sistema operacional.

`$ uname -srv` → Mostra o nome e a versão do kernel do sistema com detalhes adicionais.

### Comandos semelhantes:
`$ arch` → Mostra qual arquitetura do computador, uma possível saída é x86_64.

`# lshw | grep usb` → Com root, mostra todas as informações do sistema e periféricos que há no computador, após isso é filtrada somente as relacionadas ao usb.

---

## `uptime`

### Para que serve?
O comando `uptime` **mostra quanto tempo o sistema está no ar, a quantidade de usuário logados e a carga da CPU.**

Este comando fornece uma exibição em uma linha das seguintes informações em ordem:
- Hora atual
- Há quanto tempo o sistema está em execução.
- Quantos usuários estão conectados no momento.
- A média de carga do sistema nos últimos 1, 5 e 15 minutos.

#### Arquivos relacionados
- `/var/run/utmp` → Informações sobre quem está conectado no momento.
- `/proc` → Processo de informação. 

### Opções:
- `-p` → Mostra a quanto tempo o sistema está ligado.
- `-s` → Mostra desde quando o sistema está ligado no formato ANO-MES-DIA HORA:MINUTO:SEGUNDO

### Sintaxe comum:
**`$ uptime [OPÇÕES]`**

### Máterial Complementar:
https://www.certificacaolinux.com.br/comando-uptime-no-linux-tempo-de-atividade-guia-basico/

https://www.linuxforce.com.br/comandos-linux/comandos-linux-comando-unzip-2/