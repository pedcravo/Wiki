# Comandos de manipulação de Redes

Nesta sessão iremos ver os comandos utilizados para manipulação de redes.

### Comandos:

1. [`ab`](#ab)
2. [`aspwatch` e `iptraf`](#arpwatch-e-iptraf)
3. [`dnstop`](#dnstop)
4. [`hostname`](#hostname)
5. [`ifconfig`](#ifconfig)
6. [`ip`](#ip)
7. [`iperf`](#iperf)
8. [`mii-tool` e `ethtool`](#mii-tool-e-ethtool)
9. [`mtr`](#mtr)
10. [`netstat` e `ss`](#netstat-e-ss)
11. [`nmcli` e `nmtui`](#nmcli-e-nmtui)
12. [`ping`, `fping` e `hping`](#ping-fping-e-hping)
13. [`ssh`](#ssh)
14. [`sftp`](#sftp)

## `ab`

### Para que serve?
O comando `ab` *(Apache Benchmark)* é uma **ferramenta simples para realizar testes de carga em servidores web.** Ele é usado para medir o desempenho de um servidor HTTP em termos de número de requisições por segundo e tempos de resposta.

Essa ferramenta é útil para administradores de sistemas, desenvolvedores e profissionais de DevOps que precisam avaliar como um servidor responde a diferentes quantidades de tráfego.

#### Instalação:
`$ sudo apt install apache2-utils`

### Opções:
- `-n [N]` → Número total de requisições a serem feitas ao servidor durante o teste.
- `-c [N]` → Número de requisições simultâneas (conexões concorrentes) durante o teste.
- `-t [N]` → Duração do teste, em segundos, ignorando o número total de requisições especificado com -n.
- `-k` → Habilita a funcionalidade de Keep-Alive para conexões persistentes (reutiliza a mesma conexão para múltiplas requisições).
- `-H [HEADER]` → Adiciona cabeçalhos personalizados HTTP às requisições (como Authorization, User-Agent, etc.).
- `-p [ARQUIVO]` → Envia dados POST armazenados em um arquivo para o servidor.
- `-T [TIPO]` → Especifica o tipo de conteúdo para requisições POST (por exemplo, application/json).
- `-v [N]` → Define o nível de detalhes na saída do comando (0-4).
- `-r` → Não para o teste em caso de falhas de conexão.
- `-X [PROXY]` → Especifica um servidor proxy a ser usado durante o teste.
- `-e [ARQUIVO]` → Salva os resultados detalhados do teste em um arquivo CSV.
- `-h` → Exibe uma mensagem de ajuda e sai.

### Sintaxe comum:
**`$ ab [OPÇÕES] URL`**

### Exemplos:
`$ ab -n 100 -c10 https://www.facebook.com.br/` → Mede o desempenho do servidor `https://www.facebook.com.br/` realizando 100 requisições, com 10 requisições simultâneas.

`$ ab -n 50 -c 5 -k https://www.example.com/` → Avalia o desempenho usando conexões persistentes (Keep-Alive), reutilizando a mesma conexão para várias requisições.

`$ ab -n 20 -c 5 -p payload.json -T application/json https://api.example.com/` → Envia dados armazenados no arquivo payload.json como POST para a API com tipo de conteúdo `application/json`.

`$ ab -n 100 -c 20 -e resultados.csv https://www.example.com/` → Realiza o teste e armazena os resultados em um arquivo chamado `resultados.csv` para análise posterior.

`$ ab -n 50 -c 10 -X proxy.example.com:8080 https://www.example.com/` → Realiza o teste de carga através de um proxy configurado no endereço `proxy.example.com:8080`.

---

## `arpwatch` e `iptraf`

### Para que serve?
Os comandos `arpwatch` e `iptraf` são ferramentas de **monitoramento de rede**, cada uma com finalidades específicas. Ambos ajudam a **analisar o tráfego da rede**, mas se diferenciam em como operam e no tipo de dados que coletam.

O `arpwatch` **monitora o tráfego de rede para registrar mudanças nos endereços ARP** (Address Resolution Protocol). É usado principalmente para detectar atividades anômalas ou novos dispositivos na rede. Ao monitorar o tráfego ARP, o `arpwatch` pode alertar sobre possíveis alterações, como spoofing de ARP (quando um endereço MAC é alterado para enganar outros dispositivos na rede).

#### Principais Recursos:
- Monitoramento de endereços MAC e IP.
- Identificação de novos dispositivos conectados na rede.
- Notificações sobre mudanças de ARP para monitorar a integridade da rede.
#### Logs do arpwatch:
`/var/lib/arpwatch/enp0s3.dat`

O `iptraf` (ou sua versão mais recente `iptraf-ng`) é uma ferramenta de monitoramento em tempo real que fornece uma interface interativa para ver estatísticas de rede, como tráfego por protocolo, conexões ativas e informações de IP. É útil para a análise detalhada do tráfego de pacotes.

#### Principais Recursos:
- Estatísticas detalhadas de tráfego de rede em tempo real.
- Informações sobre conexões TCP e UDP.
- Dados sobre tráfego ICMP, monitoramento de interfaces específicas e utilização de largura de banda.

### Instalação:
`$ sudo apt install arpwatch`

`$ sudo apt install iptraf-ng`

### Exemplos:
`# systemctl start arpwatch` → Inicia o serviço `arpwatch`.

`# systemctl enable arpwatch` → Ativa o serviço arpwatch na inicialização do sistema.

`# systemctl start arpwatch@enp2s0` → Inicia o arpwatch na interface enp2s0.

`# tail /var/lib/arpwatch/enp2s0.dat` → Verifica logs do arpwatch.

`# iptraf-ng` → Inicia interface `iptraf`.

### Máterial Complementar:
<img src="https://github.com/pedcravo/Wiki/blob/main/Linux/arpwatcheiptraf.png" width="600px">

---

## `dnstop`

### Para que serve?
O comando `dnstop` é uma **ferramenta de monitoramento de tráfego DNS em tempo real.** Ele captura e exibe informações detalhadas sobre consultas e respostas DNS que passam por uma interface de rede específica. Essa ferramenta é especialmente útil para administradores de sistemas e redes que precisam monitorar e diagnosticar o tráfego DNS.

#### Notas importantes:
- **Permissões**: O dnstop geralmente requer privilégios de administrador (sudo/root) para acessar interfaces de rede.
- **Interface ou arquivo**: Sempre informe uma interface válida (como `eth0`, `wlan0`) ou um arquivo `.pcap`.
- **Modo promíscuo**: Se o tráfego completo não for exibido, use o modo promíscuo removendo a opção `-p` (ou não usando `-a`).
- **Filtros predefinidos**: Utilize os filtros com `-f` para análises específicas de consultas DNS incomuns ou malformadas. 

### Opções:
- `-4` → Monitora apenas pacotes IPv4.
- `-6` → Monitora apenas pacotes IPv6.
- `-Q` → Conta apenas consultas DNS.
- `-R` → Conta apenas respostas DNS.
- `-a` → Anonimiza endereços IP exibidos.
- `-b [EXPR]` → Define um programa BPF (Filtro de Pacotes Berkeley) para filtrar pacotes.
- `-i [ADDR]` → Ignora pacotes de um endereço IP específico.
- `-n [NOME]` → Conta apenas mensagens DNS que pertencem a um domínio específico.
- `-p` → Não coloca a interface no modo promíscuo (captura apenas pacotes destinados à máquina).
- `-r [SEGUNDOS]` → Define o intervalo de atualização da interface interativa (padrão: segundos).
- `-l [N]` → Exibe estatísticas de domínio com no máximo N componentes (por exemplo, até "subdominio.exemplo.com").
- `-X` → Desativa a tabulação de estatísticas "origem + nome de consulta".
- `-f [FILTRO]` → Aplica filtros predefinidos para análise, como:
  - `unknown-tlds` → Filtra TLDs (domínios de nível superior) desconhecidos.
  - `A-for-A` → Filtra consultas DNS A para endereços IPv4 próprios.
  - `rfc1918-ptr` → Filtra consultas PTR para endereços privados (RFC 1918).
  - `refused` → Exibe apenas respostas recusadas.
  - `qtype-any` → Filtra consultas do tipo ANY.

### Sintaxe comum:
**`$ dnstop [OPÇÕES] INTERFACE`**

**`$ dnstop [OPÇÕES] ARQUIVO`**

### Exemplos:
`$ dnstop enp2s0` → Monitora todas as consultas e respostas DNS na interface `enp2s0`.

`$ dnstop -4 enp2s0` → Exibe apenas consultas e respostas DNS usando IPv4 na interface `enp2s0`.

`$ dnstop -Q enp2s0` → Monitora apenas consultas DNS em uma interface.

`$ dnstop -R enp2s0` → Filtra respostas DNS (ignorando consultas).

---

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

## `ip`

### Para que serve?
O comando `ip` **gerencia e visualiza interfaces de rede, rotas e outras configurações IP**, proporcionando maior flexibilidade e recursos em comparação com o `ifconfig`.

#### Comparação com Comandos Antigos
1. **`ifconfig`**: Antigo comando para configuração de interfaces de rede. ifconfig foi substituído por ip por questões de funcionalidade e compatibilidade, mas ainda é encontrado em alguns sistemas.
    - Exemplo: `ifconfig` exibe detalhes das interfaces, enquanto `ip addr show` fornece uma visualização mais detalhada.
2. **`route`**: Usado anteriormente para manipular rotas IP e exibir tabelas de roteamento. Agora, ip route substitui a funcionalidade do route, fornecendo uma interface mais flexível.
    - Exemplo: `route -n` exibe rotas de forma semelhante ao `ip route show`.

### Exibindo Informações de Interfaces e Endereços
`$ ip a` ou `$ ip addr` ou `$ ip addr show` → Exibe endereços IP e informações das interfaces de rede.

`$ ip neigh` → Mostra somente endereços IP.

`$ ip a | grep inet` → Filtra a saída de `ip` mostrando somente os IPs IPV4 (`inet`) e IPV6 (`inet6`).

`$ ip link` → Manipula ou exibe o estado das interfaces de rede (se estão ativas ou inativas).

`$ ip route` → Gerencia as rotas de rede.

`$ ip -s` → Mostra estatísticas de rede.

### Configurando Endereços IP
`$ sudo ip addr add 192.168.1.108/24 dev enp2s0` → Adiciona um IP (`192.168.1.108/24`) à interface (`enp2s0`).

`$ sudo ip addr del 192.168.1.100/24 dev enp2s0` → Remove um IP da interface.

### Exibindo e Configurando Rotas
`$ ip route` ou `$ ip route show` ou `$ ip r` → Exibe a tabela de rotas.

`$ sudo ip route add 192.168.2.0/24 via 192.168.1.1` → Adiciona uma rota, com um DESTINO e um GATEWAY.

`$ ip route del 192.168.2.0/24` → Remove uma rota, utiliza somente o destino.

### Exibindo Estatísticas de Interface
`$ ip -s link` → Mostra estatísticas de pacotes, incluindo erros e pacotes descartados.

### Exemplos Adicionais para `ifconfig`, `route` e `traceroute`
`$ ifconfig enp2s0` → Exibe informações de uma interface específica.

`$ route -n` → Exibe a tabela de rotas de forma numérica.

`# traceroute fb.com` → Mostra o caminho que passamos até aquele site.

### Máterial Complementar:
<img src="https://github.com/pedcravo/Wiki/blob/main/Linux/ip.png" width="600px">

---

## `iperf`

### Para que serve?
O comando `iperf` é uma ferramenta poderosa para **medir a largura de banda da rede, latência, e desempenho da conexão entre dois pontos.** É muito usado para diagnósticos e análises de redes locais e remotas.

- Testar e medir a largura de banda da rede entre dois dispositivos (servidor e cliente).
- Suporte para conexões **TCP** e **UDP**.
- Identificar gargalos, problemas de latência, ou perda de pacotes.

### Opções:
- `-c HOST` → Define o modo cliente e conecta ao servidor `HOST` especificado.
- `-p PORTA` → Define a `PORTA` usada para a conexão (padrão: `5001`).
- `-s` → Coloca a máquina em modo servidor, aguardando conexões.
- `-u` → Usa o protocolo UDP para a transferência em vez de TCP.
- `-t [N]` → Define o tempo `N` de duração do teste, em segundos (padrão: 10 segundos).
- `-b [N]` → Define a largura `N` de banda (em UDP), por exemplo, `10M` (10 Mbps).
- `-i [N]` → Define o intervalo `N` para exibição de relatórios intermediários, em segundos.
- `-P [N]` → Realiza múltiplas conexões simultâneas (`N` sessões em paralelo).
- `--logfile=ARQUIVO` → Salva os resultados em um arquivo especificado.

### Sintaxe comum:
**`# iperf [OPÇÕES]`**

### Exemplos:
`# apt install iperf` → Instala `iperf`.

`# iperf -s` → Coloca a máquina no modo servidor, aguardando conexões.

`# iperf -c 192.168.0.17` → Mede a largura de banda TCP entre o cliente e o servidor na rede local.

`# iperf -c 192.168.0.17 -p 8080` → Conecta ao servidor na porta `8080`.

`# iperf -c 192.168.0.17 -u` → Mede a largura de banda usando o protocolo UDP.

`# iperf -c 192.168.0.17 -t 20` → Executa o teste por 20 segundos.

`# iperf -c 192.168.0.17 -u -b 5M` → Mede a largura de banda com uma taxa de 5 Mbps.

`# iperf -c 192.168.0.17 -i 2` → Mostra relatórios a cada 2 segundos durante a execução.

`# iperf -c 192.168.0.17 -P 5` → Executa 5 testes paralelos para verificar o desempenho da rede.

---

## `mii-tool e ethtool`

### Para que serve?
O comando `mii-tool` no Linux é uma ferramenta para **checar, diagnosticar e gerenciar interfaces de rede Ethernet, incluindo o status do link e a velocidade de conexão.** Pode ser usado para definir o modo de operação, como half-duplex ou full-duplex. Ele permite verificar rapidamente o estado da conexão de rede, como a velocidade de conexão e o status do link (conectado ou desconectado). `mii-tool` é utilizado, em geral, com interfaces de rede mais antigas que suportam o protocolo MII (Media Independent Interface).

No entanto, o `mii-tool` foi substituído em grande parte pelo `ethtool`, que é mais robusto e versátil, fornecendo informações detalhadas de interfaces de rede e permitindo configurações avançadas, como ajuste de offloading e tuning de filas de rede.

### Sintaxe comum:
**`$ mii-tool [OPÇÕES] INTERFACE`**

### Exemplos:
`$ lspci | grep -i ether` → Mostra as placas de rede do computador.

`$ mii-tool enp2s0` → Mostra o status da interface `enp2s0`, incluindo se o link está ativo e a velocidade da conexão (ex.: `100baseTx-FD` para `100` Mbps full-duplex).

`# mii-tool -w enp2s0` → Mantém o monitoramento contínuo de `enp2s0`, exibindo mudanças no status do link à medida que ocorrem.

`# mii-tool -F 100baseTx-HD enp2s0` → Força a interface `enp2s0` a operar a `100` Mbps em half-duplex. Pode ser útil para resolver problemas de compatibilidade em conexões.

`# mii-tool -r` → Reinicia a interface `enp2s0`.

`$ ethtool enp2s0` → Exibe informações detalhadas sobre a interface enp2s0, incluindo velocidade, modo duplex, autonegociação e suporte para diferentes recursos.

`$ ethtool -S enp2s0` → Mostra as estatísticas de pacotes enviados e recebidos.

`$ ethtool -S enp2s0 | grep -i erro` → Mostra somente as estatísticas de pacotes enviados e recebidos que contém a palavra erro. Em sua saída temos linhas como:
```bash
    tx_packets: 117800
    rx_packets: 295303
```
Que querem dizer níveis de transmissão (tx) e de recepção (rx).

---

## `mtr`

### Para que serve?
O comando `mtr` (*My Traceroute*) **combina as funcionalidades dos comandos `ping` e `traceroute`**, oferecendo uma visão detalhada do caminho de rede entre o computador do usuário e um destino especificado. Ele permite monitorar a latência e a perda de pacotes em cada salto (hop) na rota.

Ao contrário do `traceroute`, que exibe o caminho apenas uma vez, o `mtr` monitora continuamente a rota e atualiza os dados em tempo real. Isso o torna ideal para diagnosticar problemas de rede, como alta latência ou perda de pacotes.

Algumas funcionalidades do `mtr` (como o uso de TCP ou UDP) podem exigir permissões de administrador, portanto, é recomendado usar `sudo` quando necessário.

O `mtr` prioriza o uso de IPv6, mas pode ser forçado a usar IPv4 com a opção `-4`.

O modo `-r` é ideal para documentar a performance de uma rede, pois gera relatórios legíveis que podem ser exportados ou analisados.

### Opções:
- `-4` → Força o uso de endereços IPv4.
- `-6` → Força o uso de endereços IPv6.
- `-c [N]` → Especifica o número de ciclos (envios de pacotes) antes de sair.
- `-h` → Exibe uma mensagem de ajuda e encerra.
- `-r` → Gera um relatório estático (modo não interativo).
- `-s [SIZE]` → Define o tamanho dos pacotes enviados (em bytes).
- `-T` → Usa TCP em vez de ICMP para o teste de rota.
- `-U` → Usa UDP em vez de ICMP para o teste de rota.
- `-p` → Mantém as portas abertas durante os testes (útil para algumas configurações de rede).
- `-n` → Não resolve os nomes de domínio, exibindo apenas endereços IP.

### Sintaxe comum:
**`$ mtr [OPÇÕES] DESTINO`**

### Exemplos:
`$ mtr -4 google.com` → Monitora continuamente o caminho para `google.com` forçando o uso do IPv4.

`$ mtr -r -c 10 facebook.com` → Realiza 10 ciclos de teste e gera um relatório estático para `facebook.com`.

`$ mtr -T example.com` → Usa pacotes TCP em vez de ICMP para diagnosticar a rota até `example.com`.

`$ mtr -s 128 example.com` → Envia pacotes de 128 bytes ao monitorar a rota para `example.com`.

`$ mtr -n amazon.com` → Exibe os endereços IP em vez de resolver nomes de domínio ao monitorar a rota para `amazon.com`.

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

## `nmcli` e `nmtui`

### Para que serve?
Os comandos `nmcli` e `nmtui` são ferramentas de linha de comando para **gerenciar redes** no Linux. Ambos fazem parte do NetworkManager, uma ferramenta que facilita a configuração de conexões de rede, especialmente em ambientes de desktop.

O comando `nmcli` é uma interface de linha de comando que **permite ver, criar, configurar e gerenciar conexões de rede.** Útil para automatização de scripts e configuração rápida de redes em sistemas que não têm interfaces gráficas.

O comando `nmtui` é uma interface gráfica acessada a partir do terminal que fornece uma navegação por menus para **configurar redes de forma mais intuitiva.**
Ao abrir o `nmtui`, você verá um menu com opções como:
- **Editar uma conexão**: para criar ou modificar configurações de uma conexão específica.
- **Ativar uma conexão**: permite selecionar e ativar conexões salvas.
- **Definir nome do host**: permite configurar o hostname da máquina.

### Exemplos:
`$ nmcli con show` → Mostra todas as conexões de rede salvas no sistema.

`$ nmcli con show enp2s0` → Exibe detalhes da conexão de nome enp2s0.

`$ nmcli dev status` → Mostra o estado de cada dispositivo de rede (conectado/desconectado).

`$ nmcli con add con-name “dhcp” type ethernet ifname enps2s0` → Cria uma nova conexão de nome `dhcp`, tipo Ethernet, usando a interface `enp2s0`.

`$ nmcli con up “dhcp”` → Ativa a conexão `dhcp`.

`$ nmcli con down "dhcp"` → Desativa a conexão `dhcp`.

`$ man nmcli-examples` → Abre o manual com exemplos detalhados de uso do `nmcli`.

`$ nmtui` → Puxa a interface gráfica do `nmtui`.

---

## `ping`, `fping` e `hping`

### Para que serve?
Os comandos `ping`, `fping` e `hping`, que são ferramentas de rede comumente utilizadas para **diagnóstico e monitoramento de conectividade em redes IP.**

- **ping**: Verifica a conectividade com um dispositivo de rede enviando pacotes ICMP Echo (ping) e medindo o tempo de resposta.
- **fping**: Similar ao `ping`, mas permite o envio de múltiplos pings para múltiplos hosts de forma paralela, ideal para verificar rapidamente a disponibilidade de múltiplos IPs.
- **hping**: Uma ferramenta avançada que permite criar pacotes TCP/IP personalizados para testes de segurança, diagnóstico de rede, ou varredura de portas.

### Opções:
Comuns:
- `-4` → Utiliza o protocolo IPv4 para a comunicação.
- `-6` → Utiliza o protocolo IPv6 para a comunicação.
- `-c [N]` → Envia um número específico `N` de pacotes e, em seguida, para (ex.: `ping -c 3`).
- `-I` → Especifica uma interface de rede para enviar pacotes (ex.: `ping -I eth0`).
- `-b [N]` → Especifica o número de bytes de carga útil nos pacotes enviados (ex.: `ping -b 64`).

#### Específicas do `fping`
- `-g` → Permite o modo de varredura de rede, testando um intervalo de IPs (ex.: `fping -g 192.168.0.0/24`).

#### Específicas do `hping`
- `-2` → Utiliza ping em UDP.
- `-S` → Define a flag SYN, o que é útil para verificar se uma porta está aberta.
- `-p [PORT]` → Define a porta de destino do pacote.
- `-i [uN]` → Define o intervalo de envio em microssegundos (u1000 para enviar pacotes a cada 1000 microssegundos, ou 1 ms).
- `--flood` → Envia pacotes o mais rápido possível, útil para testes de estresse.

### `ping`
#### Sintaxe comum:
**`$ ping [OPÇÕES] DESTINO`**

#### Exemplos:
`$ ping 192.168.0.108` → Verificar conectividade com um IP.

`$ ping fb.com` → Verificar conectividade com um domínio.

`$ ping -c 1 fb.com -4` → Enviar 3 pacotes ICMP com IPv4.

### `fping`
#### Sintaxe comum:
**`$ fping [OPÇÕES] DESTINO`**

#### Exemplos:
`$ fping 192.168.0.108` → Mostra se o IP está ativo ou não.

`$ fping -b 12 -c 3 192.168.0.108` → Enviar 3 pacotes de 40 bytes para um IP `192.168.0.108`.

`$ fping -g 192.168.0.108` → Verificar a disponibilidade de múltiplos IPs em uma sub-rede.

### hping
#### Sintaxe comum:
**`$ hping3 [OPÇÕES] DESTINO`**

#### Exemplos:
`$ hping3 -c 100 -i u1000 192.168..0.108` → Enviar 100 pacotes ICMP a cada 1 ms.

`$ hping3 -S -p 80 192.168.0.108` → Verificar uma porta específica (ex.: porta 80).

`$ hping3 --flood -p 80 192.168.0.108` → Executar um teste de flood de pacotes.

---

## `ssh`

### Para que serve?
Utilizado para **conectar-se remotamente a outro sistema** de forma segura, através de uma conexão criptografada (chaves ssh) ou IP com senha.

O comando `ssh` (Secure Shell) permite que você **controle e administre remotamente outros computadores ou servidores**, executando comandos e transferindo arquivos com segurança.

### Chaves ssh:
São arquivos de texto que contém código criptografado, existem 2 tipos de chave:
- **chave privada** → Não deve ser compartilhada.
- **chave pública** → Pode ser compartilhada.
As chaves são salvas por padrão no diretório `~/.ssh`, local pode ser alterado pelo usuário.
Exemplos de arquivos de chaves:
- `id_rsa`: Chave privada RSA.
- `id_rsa.pub`: Chave pública RSA.

As chaves podem ser usadas para **autenticação sem senha**, copiando a chave pública para o arquivo `~/.ssh/authorized_keys` no servidor remoto.

**Trocar a porta `SSH`:** Alterar a porta padrão (22) para aumentar a segurança.

**Desabilitar login de root:** Impedir que o root faça login diretamente, exigindo que usuários usem sudo após o login com outra conta.
O local do arquivo ssh é `/etc/ssh/sshd_config`

> Ao Caso seja necessário executar um comando na máquina local, seja um `cd` ou até mesmo um `ls`, é necessário adicionar `l` de **local** antes do comando para indicar ao `ssh` que deseja executar na máquina local. Os comando `cd`, `ls` e `mkdir` ficariam assim: `lcd`, `ls` e `lmkdir`.

### Opções:
- `-C` → Habilita a compressão dos dados transmitidos, útil para melhorar o desempenho em conexões lentas.
- `-i` → Especifica o arquivo da chave privada a ser utilizado na autenticação.
- `-l` → Especifica o nome de usuário a ser utilizado na conexão.
- `-L` → Especifica o redirecionamento de portas (port forwarding) de um host local para um host remoto.
- `-N` → Inicia uma sessão SSH sem executar comandos remotos (útil para tunelamento SSH).
- `-p` → Especifica a porta a ser usada na conexão SSH (a porta padrão é 22).
- `-T` → Desabilita a alocação de pseudo-terminal (`tty`), usado quando você quer executar comandos sem iniciar um shell interativo.
- `-v` → Ativa o modo verbose, mostrando detalhes da conexão e do processo de autenticação, útil para depuração.

### Sintaxe comum:
**`$ ssh [OPÇÕES] USUARIO@host_remoto/IP`**

### Exemplos:
`$ ssh root@192.168.0.125` → Acessa o servidor, com IP `192.168.0.125` (pode ser utilizado o nome de domínio), logando como usuário **root**.

`$ ssh -i /caminho/para/chave_privada root@192.168.0.125` → Acessa o servidor com a chave privada no caminho especificado ao invés da senha.

`$ ssh root@192.168.0.125 "ls /var/logs"` → Acessa o servidor remoto, executa o comando no servidor remoto e exibe o resultado localmente.

`$ ssh -v root@192.168.0.125` → Exibe detalhes da conexão, como autenticação e handshake, útil para identificar problemas.

#### Comandos relacionados:
- `ssh-keygen` → Gera chaves privada e publica.
- `scp` → faz cópias de arquivos → `scp usuario@IP_DE_ORIGEM(REMOTO) : /arquivo /destino`.
- `ssh-agent` → Gerencia chaves SSH para evitar a necessidade de digitar a senha repetidamente.
- `ssh-add` → Carrega chaves SSH no agente para autenticação automática.
  
### Gerar chaves ssh:
`$ ssh-keygen` → Gera chaves privada e publica.

`# ssh-keygen -b 1024 -t rsa` → Cria chaves `pub` e `priv` com tamanho de `1024` bits do tipo `rsa` de segurança.

`$ ssh-copy-id root@IP` → Faz uma cópia da chave publica da máquina para o servidor.

`$ ssh-copy-id -i /caminho/para/chave_privada root@IP` → Faz uma cópia da chave publica do diretório especificado para o servidor.

`$ scp arquivo root@192.168.0.125:/caminho/destino` → Faz cópias de arquivos de forma segura entre máquinas.

`$ nano /etc/ssh/sshd_config` → Usado para editar arquivo com configurações do ssh.

### Ligar e desligar ssh:
`$ sudo systemctl start sshd` → Inicia o serviço de ssh servidor.

`$ sudo systemctl enable sshd` → Habilita o serviço na carga do sistema operacional no ssh servidor.

`$ sudo systemctl status ssh` → Verifica o status do serviço ssh.

`$ sudo systemctl disable ssh` → Desabilita o serviço ssh, de modo que ele não será iniciado automaticamente quando o sistema for reiniciado.

`$ sudo systemctl disable --now ssh` → Desabilita o serviço ssh, de modo que ele não será executado a partir de agora.

`$ sudo systemctl enable ssh` → Habilita o serviço ssh, de modo que ele será iniciado automaticamente quando o sistema for reiniciado.

`$ sudo systemctl enable --now ssh` → Habilita o serviço ssh, de modo que ele será executado a partir de agora.

### Máterial Complementar:
https://www.youtube.com/watch?v=a2BVQ42CQyA

https://www.youtube.com/watch?v=NqW-BeYRBkE]

https://www.certificacaolinux.com.br/comando-linux-ssh/

Aula 1 - Acesso remoto do servidor e host usando SSH.txt

Aula 2 - Trabalhando com chaves Assimétricas.txt

---

## `sftp`

### Para que serve?
O comando `sftp` é utilizado para **manipular arquivos entre servidor e máquina local.**

O `sftp` é um subsistema do `ssh`. Portanto, ele **suporta todos os métodos de autenticação `ssh`.** Enquanto pode ser fácil configurar e usar autenticação por senha, é muito mais conveniente e seguro criar chaves `ssh` para ter um login de sftp sem senha.

A conexão ao servidor é feita de forma semelhante ao comando `ssh`, é necessário o usuário e o endereço de IP (ou nome do domínio).

### Opções:
- `-oPort=N` → Seleciona a porta `N` para se conectar, caso a porta seja diferente da porta padrão.

### Comandos quando conectado:
A maioria dos comandos para manipulação de arquivos, como `cd`, `ls`, `mkdir` e `rmdir`, necessitam que seja adicionado `l` de local antes do comando para indicar ao `ssh` que deseja executar na máquina local.
Porém existem exceções, como os comandos `rm`, `chown`, `chgrp` e `chmod`,  que funcionam apenas no sistema remoto.
- `get` → Comando utilizado para importar um arquivo do arquivo do servidor para a máquina local.
- `mget` → Comando utilizado para importar diversos arquivos do servidor para a máquina local.
- `put` → Comando utilizado para exportar um arquivo da máquina local para o servidor.
- `mput` → Comando utilizado para exportar vários arquivos da máquina local para o servidor.
- `df -h` →Comando utilizado para conferir o espaço em disco de um servidor remoto em gigabytes.
- `rename` → Comando utilizado para renomear arquivos.
- `bye` ou `exit` → Comandos utilizados para sair do `sftp`.

### Sintaxe comum:
**`$ sftp [OPÇÕES] USUARIO@host_remoto/IP`**

### Exemplos:
`$ sftp pedro@192.168.0.129` → Conecta ao servidor de IP: `192.168.0.129`, como o usuário pedro.

`$ sftp -oPort=22022 pedro@192.168.0.129` → Conecta ao servidor de IP: `192.168.0.129`, como o usuário pedro, pela porta 22022.

### Sintaxe comum para transferência de arquivos:
**`sftp> COMANDO /DirOriginal/arquivo /DirDestino/`**

`sftp> get /etc/xinetd.conf` → Importa arquivo `/etc/xinetd.conf` do servidor para o diretório atual da máquina local.

`sftp> get file.txt /home/pedro/Downloads` → Importa arquivo `file.txt` do servidor para o diretório `/home/pedro/Downloads` da máquina local.

`sftp> mget /etc/*.conf` → Importa todos os arquivos com `.conf` do diretório `/etc` do servidor  para o diretório atual da máquina local.

`sftp> put /home/pedro/imagem.png /root` → Exporta arquivo `/home/pedro/imagem.png` da máquina local para o diretório `/root` no servidor.

`sftp> mput /home/pedro/*.txt` → Exporta arquivo todos os arquivos `.txt` da máquina local para o diretório atual do servidor.

`sftp> pwd` → Executa o comando pwd no servido.

`sftp> lpwd` → Executa o comando pwd na máquina local.

`sftp> ls` → Executa o comando ls no servido.

`sftp> lls` → Executa o comando ls na máquina local.

`sftp> rename A.txt B.txt` → Renomeia o arquivo `A.txt` para `B.txt`.

### Máterial Complementar:
https://www.hostinger.com.br/tutoriais/como-usar-sftp-ssh-file-transfer-protocol

https://www.linuxforce.com.br/comandos-linux/comandos-linux-comando-sftp/

<img src="https://github.com/pedcravo/Wiki/blob/main/Linux/.png" width="600px">

---