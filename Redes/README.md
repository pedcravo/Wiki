# Redes
Nesta seção iremos abordar o assunto de Redes. Como funcionam, quais seus protocólos, aplicações, dentre outras tecnologias relacionadas.

## Tópicos
- [Redes](#redes)
  - [Tópicos](#tópicos)
  - [Protocolos](#protocolos)
    - [TCP](#tcp)
    - [UDP](#udp)
  - [Aplicações](#aplicações)
    - [Telnet](#telnet)
  - [Arquiteturas](#arquiteturas)
    - [Client-Server](#client-server)
  
## Protocolos
### TCP
Protocolo de rede utilizado para receber e envir mensagens.

Arquitetura [Client-Server](#client-server).

\- Veloz porém + Utilizado.

### UDP
Protocolo de rede utilizado para enviar mensagens, sem se importar para quem ou se há alguém que recebe.

\+ Veloz porém - Utilizado.


## Aplicações
### Telnet
Aplicação de mensageria que utiliza do protocolo [TCP](#tcp).

## Arquiteturas
### Client-Server
Arquitetura de redes onde uma aplicação que está no ar faz "bind" de uma porta (server) para que outra se conecte a ela (client) e se comuniquem.

> bind → Tornar uma porta ("socket") exclusiva daquela aplicação, onde os clients vão acessar somente ela atráves da porta.

> socket → Uma estrutura que que torna possível a conexão online com servidores, máquinas, dentre outros.