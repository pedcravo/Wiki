# Comandos de manipulação do sistema

Nesta sessão vamos ver os comandos que são utilizados para manipular o sistema, ou seja, os comandos que mexem nas configurações do sistema e dos processos.

### Comandos:

1. [`&`](#&)
2. [`at`](#at)
3. [`bg`](#bg)
4. [`fg`](#fg`)
5. [`cron` e `anacron`](#cron-e-anacron)
6. [`date`](#date)
7. [`dnstop`](#dnstop)
8. [`fdisk`](#fdisk)
9. [`free`](#free)
10. [`history`](#history)
11. [`hostname`](#hostname)
12. [`htop`](#htop)
13. [`ifconfig`](#ifconfig)
14. [`ionice`](#ionice)
15. [`iostat`](#iostat)
16. [`iperf`](#iperf)
17. [`jobs`](#jobs)
18. [`kill`](#kill)
19. [`mii-tool` e `ethtool`]()
20. [`modprobe`]()
21. [`mount` e `unmount`]()
22. [`nice`]()
23. [`renice`]()
24. [`nmcli` e `nmtui`]()
25. [`pgrep`]()
26. [`ps`]()
27. [`pstree`]()
28. [`rsync`]()
29. [`sar`]()
30. [`sftp`]()
31. [`ssh`]()
32. [`swapon`]()
33. [`systemctl`]()
34. [`tmux`]()
35. [`top`]()
36. [`tty`]()
37. [`tzselect`]()
38. [`uname`]()
39. [`uptime`]()
40. [`vmstat`]()

## `cron` e `anacron`

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

---

##

### Para que serve?

### Opções:

### Sintaxe comum:

### Exemplos:

### Máterial Complementar:
