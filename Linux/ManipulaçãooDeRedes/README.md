## `hostname`

### Para que serve?
O comando `hostname` no Linux é usado para **exibir ou configurar o nome do host (hostname)** da máquina, que é o nome usado para identificar o computador em redes. Este comando permite também consultar informações de rede relacionadas ao hostname, como IP e domínio.

O nome do **host** pode ser temporariamente alterado no terminal com `hostname`, mas para configurações permanentes, ele deve ser configurado no arquivo `/etc/hostname` ou usando ferramentas apropriadas do sistema (como `hostnamectl` em distribuições com `systemd`).

### Opções:
- `-d` → Mostra o nome do domínio associado ao hostname.
- `-f` → Mostra o hostname completo (FQDN - Fully Qualified Domain Name), se estiver configurado.
- `-i` → Exibe o endereço IP associado ao hostname atual.
- `-v` → Exibe a versão do programa `hostname`.

### Exemplos:
`$ hostname` → Exibe o hostname atual do sistema.

`$ sudo hostname backend` → Configura o hostname temporariamente para `backend` até a próxima reinicialização.

`$ hostname -i` → Exibe o endereço IP associado ao hostname atual.

`$ hostname -f` → Mostra o hostname completo, se estiver configurado.

`$ hostname -d` → Mostra o nome do domínio associado ao hostname.

`$ hostname -v` → Exibe a versão do programa `hostname`.


`$ sudo nano /etc/hostname` → Define o hostname de maneira permanente, edite o arquivo `/etc/hostname` com o novo nome.


`$ sudo hostnamectl set-hostname frontend` → Em sistemas com `systemd`, o comando `hostnamectl` também pode ser usado para definir o hostname.

### Máterial Complementar:
<img src="https://github.com/pedcravo/Wiki/blob/main/Linux/hostname.png" width="600px">

---

## `ifconfig`

### Para que serve?
Usado comummente para Verificar o IP.

### Exemplos:
`$ ifconfig | grep inet` → Filtra as linhas com `inet` (linhas que contém o IP).

`$ ip a s` → Mostra o mesmo que o `ifconfig` porém de forma menos organizada.

### Máterial Complementar:
<img src="https://github.com/pedcravo/Wiki/blob/main/Linux/ifconfig.webp" width="600px">

https://www.ibm.com/docs/pt-br/aix/7.3?topic=i-ifconfig-command

https://www.certificacaolinux.com.br/comando-linux-ifconfig/

https://www.linuxforce.com.br/comandos-linux/comandos-linux-comando-ifconfig/

---