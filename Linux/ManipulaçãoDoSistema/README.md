---

## 11. `uniq`

### Para que serve?

### Opções:

### Sintaxe comum:

### Exemplos:

### Máterial Complementar:

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

---
