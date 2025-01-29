# Redis
Nesta seção iremos falar sobre Redis. O que ele é, para que serve, comandos uteis, dentre outras coisas uteis deste programa.

## Tópicos
- [Redis](#redis)
  - [Tópicos](#tópicos)
  - [Conceitos:](#conceitos)
    - [Redis](#redis-1)
    - [Redis Commander](#redis-commander)
    - [Redis AOF \& RDB](#redis-aof--rdb)
    - [Redis Replication](#redis-replication)
    - [Redis Sentinel](#redis-sentinel)
      - [Exemplo de Arquitetura:](#exemplo-de-arquitetura)
    - [Redis Cluster](#redis-cluster)
    - [Replication VS Cluster](#replication-vs-cluster)
    - [Pub/Sub](#pubsub)
      - [Canais comuns:](#canais-comuns)
      - [Canais por padrão:](#canais-por-padrão)
  - [KEYS](#keys)
      - [Comandos gerais:](#comandos-gerais)
    - [String](#string)
      - [Comandos de String no redis:](#comandos-de-string-no-redis)
      - [Exemplos de uso:](#exemplos-de-uso)
    - [Hash](#hash)
      - [Comandos de Hash no redis:](#comandos-de-hash-no-redis)
      - [Exemplos de uso:](#exemplos-de-uso-1)
    - [Listas](#listas)
      - [Comandos de  no redis:](#comandos-de--no-redis)
      - [Exemplos de uso:](#exemplos-de-uso-2)
    - [Conjuntos (Sets)](#conjuntos-sets)
      - [Comandos de Sets no Redis:](#comandos-de-sets-no-redis)
      - [Exemplos de uso:](#exemplos-de-uso-3)
    - [Conjuntos Classificados (Sorted Sets)](#conjuntos-classificados-sorted-sets)
      - [Comandos de Sorted Sets no Redis:](#comandos-de-sorted-sets-no-redis)
      - [Exemplos de uso:](#exemplos-de-uso-4)
    - [JSON](#json)
      - [Comandos de JSON no Redis:](#comandos-de-json-no-redis)
      - ["$" vs "."](#-vs-)
        - ["$"](#)
        - ["."](#-1)
      - [Exemplos de JSON:](#exemplos-de-json)
  - [Redis no Docker:](#redis-no-docker)
  - [Instalação e Configurações:](#instalação-e-configurações)
  - [redis.conf](#redisconf)
  - [Recursos Úteis](#recursos-úteis)

## Conceitos:
### Redis
**Redis** é um banco de dados no SQL, que armazena dados na memória do computador, mais especificamente na memória ativa do computador, o que é mais rápido do que acessar dados em armazenamento secundário, como um disco rígido.

<img src="https://github.com/pedcravo/Wiki/blob/main/Redis/RedisIsFast.jpg" width="600px">


### Redis Commander
**Redis Commander** é um programa que utiliza a porta 8081 da máquina para visualizar os dados do **Redis** e fazer comandos diretamente no mesmo usando a linha de comando na parte inferior da página.

> Para acessar o Redis Commander no navegador, acesse http://localhost:8081/
> 
> O usuário e a senha são ***admin***.

### Redis AOF & RDB
|            **Nome**             | **O que faz?**                                                                                                                                       | **Tempos para execução**                                                                                                                                    | **Vantagens**                                                                                    |
| :-----------------------------: | :--------------------------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------- |
|   Append-Only File (**AOF**)    | È um sistema de backup que baixa cada log, cada operação em um arquivo (.aof).                                                                       | **Sempre** - Baixa performace porém alta segurança; **A Cada Segundo** - Performace melhor e segurança média; **Desligado** - Melhor performace e inseguro. | Mais confiável pois cada log foi salvo no arquivo.                                               |
| Redis Database Backup (**RDB**) | É um sistema de backup semelhante ao Git que faz snapshots do Redis e os organiza em ordem cronológica arquivos binários (dump.rdp), pode ter forks. | A cada 1 minuto se 10 alterações; 5 minutos se 1000 alterações.                                                                                             | Não afeta performace do Redis; Velocidade alta para restauração de dados; Arquivo mais compacto. |

[Vídeo sobre AOF e RDB →][video7]

[Fazer backup →][rdp&aof]


### Redis Replication
O **Redis Replication** é um recurso que permite replicar os dados de um servidor Redis (conhecido como primary ou master) para outros servidores (conhecidos como replicas ou slaves). Ele permite que as instâncias replicas Redis sejam cópias exatas das instâncias mestras. A réplica se reconectará automaticamente ao mestre toda vez que o link quebrar e tentará ser uma cópia exata dela, independentemente do que acontecer com o mestre. Essa replicação é usada para aumentar a disponibilidade, a escalabilidade e a redundância dos dados em um ambiente Redis.

Muitas réplicas conectadas podem sobrecarregar o primary, especialmente durante sincronizações iniciais, em outras palavras o Failover.

[Vídeo sobre Redis Replication e Cluster →][video4]


### Redis Sentinel
O **Redis Sentinel** é um sistema integrado ao Redis que fornece alta disponibilidade para ambientes distribuídos. Ele é responsável por monitorar instâncias Redis (master e replicas), detectar falhas, realizar failover automático e configurar os clientes para que eles sempre acessem o primary correto.

Quando o master falha, os Sentinels escolhem uma réplica para ser promovida a primary com base em critérios como o tempo de atraso na replicação.
Após a promoção, os Sentinels reconfiguram as outras replicas para replicarem o novo primary.

#### Exemplo de Arquitetura:
- Um primary Redis.
- Duas replicas Redis.
- Três instâncias Redis Sentinel (em servidores diferentes) para monitorar o cluster.

**Quando o primary falha:**
1. O Sentinel detecta a falha.
2. Um consenso é alcançado entre os Sentinels para iniciar o failover.
3. Uma réplica é promovida a primary.
4. As réplicas restantes são configuradas para sincronizar com o novo primary.
5. Os clientes são informados sobre o novo primary.

[Vídeo sobre Redis Sentinel →][video5]


### Redis Cluster
O **Redis Cluster** é uma funcionalidade do Redis que permite distribuir dados entre múltiplos nós, ***oferecendo escalabilidade horizontal*** e alta disponibilidade. Ele é projetado para lidar com grandes volumes de dados e alta taxa de requisições, dividindo a carga entre vários servidores e mantendo os dados disponíveis mesmo em caso de falhas.

Cada nó pode ter réplicas (chamadas de replica nodes ou slaves). Essas réplicas são usadas para garantir que os dados permaneçam acessíveis em caso de falha de um nó primário (master). Se um nó primário falhar, uma de suas réplicas é promovida automaticamente a primário.

É possível adicionar ou remover nós do cluster dinamicamente, redistribuindo os slots para equilibrar a carga.

[Vídeo sobre Redis Cluster →][video6]


### Replication VS Cluster
|    **Redis**    | **O que faz?**                                                                                 | **Monitoramento de Failover**                          |
| :-------------: | :--------------------------------------------------------------------------------------------- | :----------------------------------------------------- |
| **Replication** | Replica mudanças feitas no master em suas replicas, salva em mais de um local os mesmos dados. | Não faz sozinho, precisa do **Redis Sentinel**.        |
|   **Cluster**   | Distribui os dados entre máquinas, divide os dados em 16k slots (chamados de hash slots).      | Faz automáticamente caso os Clusteres tenham réplicas. |


### Pub/Sub
[**Pub/Sub**][pubsub], ou **Publish/Subscribe** em outras palavras, **é uma forma de envio e recepção de mensagens que existe no Redis**. Esse método pode ser usado entre máquinas ou aplicações.
Este método consiste em uma máquina (por exemplo), que como Publisher envia mensagens e uma ou mais máquinas como Subscriber recebem essas mensagens.

[Vídeo sobre Pub/Sub →][video3]

#### Canais comuns:
**SUBSCRIBE** → Assina um ou mais canais.
``` bash
> SUBSCRIBE channel <channel>
```
**Saída:**
```bash
1) "subscribe"
2) "channel"
3) (integer) n
```
1. Mostra o comando que foi executado com sucesso, foi possível conectar a um ou mais canais.
2. Mostra o nome do canal.
3. Mostra a quantidade `n` de canais assinados.
**Recebendo mensagens:**
```bash
1) "message"
2) "channel"
3) "Hello World"
```
1. Mostra que o comando `PUBLISH` foi executado com sucesso pelo PUBLISHER.
2. Mostra o nome do canal.
3. Mostra a mensagem enviada.


**PUBLISH** → Envia mensagem aos SUBSCRIBERS pelos canais.
``` bash
> PUBLISH channel message
```
**Saída:**
```bash
(integer) n
```
1. Mostra que o comando foi executado com sucesso, a mensagem foi enviada com sucesso.


**UNSUBSCRIBE** → Deixa de assinar um ou mais canais.
``` bash
> UNSUBSCRIBE <channel <channel ...>>
```
**Saída:**
```bash
1) "unsubscribe"
2) "channel"
3) (integer) n
```
1. Mostra o comando que foi executado com sucesso, foi possível desconectar de um ou mais canais.
2. Mostra o nome do canal.
3. Mostra a quantidade `n` de canais assinados, caso seja menor que 0 não há nenhum canal assinado.

#### Canais por padrão:
**PSUBSCRIBE** → Assina um padrão de canais utilizando padrão de caracteres e [**meta caracteres**][metacaractere] como `*`, `?` e `[]`.
``` bash
> PSUBSCRIBE pattern <pattern>
```

**Saída:**
```bash
1) "psubscribe"
2) "pattern"
3) (integer) n
```
1. Mostra o comando que foi executado com sucesso, foi possível conectar a um padrão canais.
2. Mostra o padrão dos canais conectados.
3. Mostra a quantidade `n` de canais assinados.
**Recebendo mensagens:**
```bash
1) "pmessage"
2) "pattern"
3) "channel"
4) "Hello World"
```
1. Mostra que o comando `PUBLISH` foi executado com sucesso pelo PUBLISHER.
2. Mostra o padrão usado.
3. Mostra o nome do canal que foi enviada a mensagem.
4. Mostra a mensagem enviada.


**PUNSUBSCRIBE** → Deixa de assinar um ou mais canais.
``` bash
> UNSUBSCRIBE <pattern <pattern ...>>
```
**Saída:**
```bash
1) "punsubscribe"
2) "pattern"
3) (integer) n
```


## KEYS
**Key** são chaves atreladas a valores, cada chave tem seu **nome**, seu **tempo de vida** (TTL) e seu **tipo**.

**Dois pontos (:)** é uma forma de criar pastas e inserir os tipos de dados desejados, **pode ser usado na criação de qualquer um dos tipos de dados**. Forma base `pasta:key`, futuramente iremos ver exemplos.

**Pipeline é uma otimização que ajuda a executar vários comandos no Redis sequencialmente.** Normalmente, para uma interação do Redis, um cliente primeiro emite um comando para o servidor e, em seguida, envia outro quando o processamento do seu comando é concluído.
Em contraste com o Redis Pipelining, os clientes podem enviar vários comandos de uma vez para o servidor sem esperar por cada resposta. Para isso, o servidor armazena esses comandos e os processa serialmente antes de retornar a resposta após executar todos os comandos.

#### Comandos gerais:
- `KEYS name` → **Pesquisa chaves**, idependente do tipo, é possível utilizar os metacaracteres de forma semelhante ao terminal do linux.
- `TYPE key` → **Verifica o tipo** da chave.
- `INFO section` → **Fornece informações detalhadas e estatísticas** sobre o servidor, incluindo o uso de memória, carga da CPU, clientes conectados, status de replicação e muito mais.
- `EXPIRE key` → **Dá um TTL** para uma chave.
- `TTL key` → **Verifica o TTL** da chave.
- `MULTI` → **Inicia o Pipeline** dando inicio a lista dos comandos.
- `EXEC` → **Finaliza Pipeline e executa.**
- `DESCARTE` → **Cancela o bloco de transações** criado por `MULTI`, descartando todos os comandos enfileirados.
- `MONITOR` → **Fornece um feed em tempo real** de todos os comandos executados no servidor, exibindo cada comando junto com seus argumentos à medida que são processados.

---
### String
As strings são o tipo de dado mais simples no Redis e armazenam valores únicos associados a uma chave.

> **Uma** chave é liga a **um** valor.

#### Comandos de String no redis:
- `SET key value` → Define uma chave com o valor.
- `GET key` → Retorna o valor da chave.
- `DEL key` → Remove a chave.
- `INCR key` → Incrementa o valor em 1 (assumindo que é numérico).
- `DECR key` → Decrementa o valor em 1 (assumindo que é numérico).
- `APPEND key value` → Adiciona texto ao final do valor existente.

#### Exemplos de uso:
```bash
SET name João
GET name
DEL name
```
1. Define uma chave "name" com o valor "João".
2. Retorna o valor da chave "name".
3. Remove a chave "name".

```bash
SET name:1 João
GET name:1
SET name:2 Thiago
GET name:2
SET name:3 Pedro
GET name:3
```
1. Cria uma pasta chamada "name" e insere uma chave "1" com o valor "João".
2. Retorna o valor da chave "1" na pasta "name".
3. Insere na pasta chamada "name" uma chave "2" com o valor "Thiago".
4. Retorna o valor da chave "2" na pasta "name".
5. Insere na pasta chamada "name" uma chave "3" com o valor "Pedro".
6. Retorna o valor da chave "2" na pasta "name".

```bash
SET counter 10
INCR counter
DECR counter
APPEND counter " vezes"
GET counter
```
1. Define uma chave "counter" com o valor "10".
2. Incrementa o valor da chave "counter" para "11".
3. Decrementa o valor da chave "counter" para "10".
4. Adiciona o texto " vezes" ao valor, resultando em "10 vezes".
5. Retorna o valor atualizado.

---
### Hash
Os hashes armazenam coleções de pares **campo/valor**, similares a um objeto JSON.
É possível inserir mais de um campo/valor por comando.

> **Uma** chave está ligada a um **conjunto** de campos e valores.

#### Comandos de Hash no redis:
- `HSET key field value` → Define um campo e valor no hash.
- `HGET key field` → Retorna o valor de um campo específico.
- `HGETALL key` → Retorna todos os campos e valores do hash.
- `HDEL key field` → Remove um campo do hash.
- `HLEN key` → Retorna o número de campos no hash.
- `HEXISTS key field` → Verifica se um campo existe.

#### Exemplos de uso:
```bash
HSET user:1 name João
HSET user:1 age 30
HGET user:1 name
HGETALL user:1
```
1. Define um hash "1" na pasta "user" com o campo "name" e valor "João".
2. Adiciona o campo "age" com o valor "30".
3. Retorna o valor do campo "name".
4. Retorna todos os campos e valores do hash "user:1".

```bash
HSET user:2 login teste senha teste123 pontos 200
HGETALL user:2
```
1. Insere um hash "user:2" com os campos "login" com valor "teste", "senha" com valor "teste123", "pontos" com valor "200".
2. Mostra todos os campos e valores do hash "user:2".

---
### Listas
As listas armazenam uma sequência ordenada de valores (strings).

> **Uma** chave está ligada a **uma lista** ordenada de valores.

#### Comandos de <Tipo de dado> no redis:
- `LPUSH key value` → Adiciona um valor ao início da lista.
- `RPUSH key value` → Adiciona um valor ao final da lista.
- `LPOP key` → Remove e retorna o primeiro elemento da lista.
- `RPOP key` → Remove e retorna o último elemento da lista.
- `LRANGE key start stop` → Retorna elementos de uma faixa da lista.

#### Exemplos de uso:
```bash
LPUSH tasks "Estudar Redis"
LPUSH tasks "Ler Documentação"
RPUSH tasks "Praticar"
LRANGE tasks 0 -1
```
1. Adiciona "Estudar Redis" ao início da lista "tasks".
2. Adiciona "Ler Documentação" ao início da lista "tasks".
3. Adiciona "Praticar" ao final da lista "tasks".
4. Retorna todos os elementos da lista.

---
### Conjuntos (Sets)
Os conjuntos armazenam valores únicos e não ordenados. É possível adicionar mais de um dado ao mesmo tempo.

> **Uma** chave está ligada a um **conjunto** de valores únicos.

#### Comandos de Sets no Redis:
- `SADD key value` → Adiciona um valor ao conjunto.
- `SMEMBERS key` → Retorna todos os valores do conjunto.
- `SCARD key` → Retorna o número de elementos no conjunto.
- `SREM key value` → Remove um valor do conjunto.
- `SISMEMBER key value` → Verifica se um valor está no conjunto.

#### Exemplos de uso:
```bash
SADD tags Redis NoSQL Database
SMEMBERS tags
SCARD tags
```
1. Adiciona "Redis", "NoSQL" e "Database" ao conjunto "tags".
2. Retorna todos os valores do conjunto "tags".
3. Retorna o número de elementos no conjunto.

```bash
SADD user:1:teste redis
SADD user:1:teste mongodb
SADD user:1:teste mysql
SCARD user:1:teste    
```
1. Define um hash "user:1:teste" com o valor "redis".
2. Adiciona o valor "mongodb" ao hash.
3. Adiciona o valor "mysql" ao hash.
4. Mostra a quantidade de dados no hash "user:1:teste".

---
### Conjuntos Classificados (Sorted Sets)
Os conjuntos classificados são como conjuntos, mas cada valor está associado a um score numérico para ordenação.
É possível inserir mais de um valor/score por comandos.

> **Uma** chave está ligada a um **conjunto** ordenado de valores com scores (pontos).

#### Comandos de Sorted Sets no Redis:
- `ZADD key score value` → Adiciona um valor com um score ao conjunto.
- `ZINCRBY key increment value`
- `ZRANGE key start stop [WITHSCORES]` → Retorna valores dentro de uma faixa de índices de forma crescente, com ou sem scores ([WITHSCORES]).
- `ZRANGEBYSCORE key min max` → Retorna valores dentro de uma faixa de scores de forma decrescente, com ou sem scores ([WITHSCORES]).
- `ZREM key value` → Remove um valor do conjunto.
- `ZRANK key value` → Mostra qual a posição daquele value em relação ao ranking, onde o maior rank é o de maior score.
- `ZREVRANK key value` → Mostra qual a posição daquele value em relação ao ranking ao contrário, onde o menor rank é o de maior score.
- `ZSCORE key value` → Mostra qual o score daquele value.

#### Exemplos de uso:
```bash
ZADD leaderboard 100 Pedro
ZADD leaderboard 200 João
ZRANGE leaderboard 0 -1 WITHSCORES
```
1. Adiciona "Pedro" ao conjunto "leaderboard" com score 100.
2. Adiciona "João" ao conjunto "leaderboard" com score 200.
3. Retorna todos os valores com seus scores.

---
### JSON
O tipo de dado JSON no Redis é usado para armazenar documentos JSON diretamente, permitindo manipulação e consulta de seus campos. Esse tipo é suportado por meio do módulo **RedisJSON**.

> **Uma** chave está ligada a **um documento** JSON.

#### Comandos de JSON no Redis:
- `JSON.SET key path value` → Define um valor no caminho especificado no documento JSON.
- `JSON.ARRAPPEND key path value` → Adiciona um valor ao final de um array JSON.
- `JSON.GET key [path]` → Retorna o documento JSON inteiro ou parte dele.
- `JSON.DEL key [path]` → Remove o documento JSON ou parte dele.
- `JSON.TYPE key [path]` → Retorna o tipo do valor no caminho especificado.

#### "$" vs "."
<img src="https://github.com/pedcravo/Wiki/blob/main/Redis/RedisJSON.png" width="600px">

##### "$"
O $ é usado como o caminho raiz quando você deseja acessar ou manipular dados de um JSON existente. Ele funciona como o ponto de partida para selecionar partes específicas do documento.

**Características do $:**
- Utilizado principalmente em comandos que leem ou manipulam partes de um JSON já armazenado.
- Representa todo o documento ou caminhos dentro dele.
- Suporta seleção de múltiplos elementos ou valores específicos em estruturas complexas.

```bash
JSON.GET vendor:96 $
JSON.GET vendor:96 $.name
JSON.GET vendor:96 $.menu[*].name
```
1. Retorna todo o JSON armazenado na chave "vendor:96".
2. Retorna o valor do campo "name".
3. Retorna uma lista com os valores do campo "name" dentro de todos os itens do array "menu".

##### "."
O . é usado para definir diretamente o caminho ao criar ou atualizar um JSON novo ou existente. Ele especifica a hierarquia de campos no documento.

**Características do ".":**
- Utilizado para criar ou atualizar valores em partes específicas de um JSON.
- Representa o ponto no qual você está inserindo/modificando dados.
- Não é usado para leitura de dados (apenas para escrita).

```bash
JSON.SET vendor:96 . '{"name":"Tacos Mi Ranchos"}'
JSON.SET vendor:96 .location '{"address":"123 Main St"}'
JSON.SET vendor:96 .menu[0] '{"name":"burrito","price":11.5}'
```
1. Cria um JSON inteiro com o campo "name".
2. Adiciona um novo campo "location" com um objeto contendo "address".
3. Substitui o primeiro elemento do array "menu".

#### Exemplos de JSON:
```bash
JSON.SET user:1 $ '{"name":"João","age":30,"skills":["Redis","Docker"]}'
JSON.GET user:1
JSON.GET user:1 $.name
JSON.SET user:1 $.age 31
JSON.ARRAPPEND user:1 $.skills "Kubernetes"
JSON.GET user:1 $.skills
```
1. Define um documento JSON para a chave "user:1" contendo os campos "name", "age" e "skills".
2. Retorna o documento JSON completo associado à chave "user:1".
3. Retorna o valor do campo "name" no documento JSON.
4. Atualiza o campo "age" para 31.
5. Adiciona o valor "Kubernetes" ao array "skills".
6. Retorna o array atualizado de "skills".

```bash
JSON.SET vendor:96 . '
{
   "name": "Tacos Mi Ranchos",
   "phone": 5557891234,
   "menu":
        [
           {
              "name": "burrito",
              "price", 11.5
            },
           {
              "name": "taco",
              "price", 3.5
            },
       ]
}'

JSON.SET vendor:96 .location '
{
   "address": "1434 1st Ave, Oakland, CA 94606",
   "coordinates":
       [
          37.7989708,
          -122.2565053
       ]
}'

JSON.SET vendor:96 .location.address "\" 1452 1st Ave, Oakland, CA 94606\""

JSON.GET vendor:96
```
1. Define o JSON inicial, cria a estrutura com "name", "phone" e "menu" com dois itens.
2. Adiciona o campo "location", insere o endereço original e as coordenadas de localização.
3. Atualiza o endereço em "location", modifica o campo "address" de "1434" para "1452".
4. Exibe o documento JSON completo, o comando final retorna o documento completo armazenado na chave "vendor:96".

> Para mais sobre **JSON** acesse:
> - [RedisJSON documentação →][jsondoc]
> - [Video Redis and JSON Explained →][video1]
> - [Vídeo Redis and JSON Explained (Revisited) →][video2]

## Redis no Docker:
Caso o **Redis** esteja sendo executado via [**Docker**][docker], o comando para acessar a linha de comando do **Redis** é diferente de se o **Redis** estivesse diretamente na máquina. Podemos observar isso:

| **Local do Redis** | **Comando**                                |
| :----------------: | :----------------------------------------- |
|      Máquina       | `$ redis-docker redis-cli`                 |
|       Docker       | `$ docker exec -it redis-docker redis-cli` |

## Instalação e Configurações:
Para fazer a instalação e configurações do **Redis** e do **Redis Commander** é indicado o uso em [**Docker**][docker].
Então primeiramente faça a instalação do [**Docker**][docker] em sua máquina.

Após instalar o **Docker** execute os comandos em [**Instalação docker, redis, redis commandar e sql**][tutorial].

## redis.conf
Acesse as configurações básicas de redis.conf https://raw.githubusercontent.com/redis/redis/unstable/redis.conf

[Explicação das configurações →][redisconfig]

[Fazer backup →][rdp&aof]

## Recursos Úteis
<img src="https://github.com/pedcravo/Wiki/blob/main/Redis/RoadmapRedis.png" width="600px">

[**Roadmap sobre Docker →**][roadmap]

[**Pub/Sub →**][pubsub]

[**Documento sobre JSON →**][jsondoc]

[**Vídeo Redis and JSON Explained →**][video1]

[**Vídeo Redis and JSON Explained (Revisited) →**][video2]

[**Vídeo Redis pubsub →**][video3]

[**Vídeo Redis Replication →**][video4]

[**Vídeo Redis Sentinel →**][video5]

[**Vídeo Redis Cluster →**][video6]

[**Vídeo sobre AOF e RDB →**][video7]

[**Fazer backup →**][rdp&aof]

[**Tutorial do Luiz →**][tutorial]

[**Anotações sobre Docker →**][docker]

[**Explicação das configurações →**][redisconfig]

[docker]: https://github.com/pedcravo/Wiki/tree/main/Docker
[tutorial]: https://github.com/LuizFillipe1/dicas
[jsondoc]: https://redis-io.translate.goog/docs/latest/develop/data-types/json/?_x_tr_sl=en&_x_tr_tl=pt&_x_tr_hl=pt&_x_tr_pto=tc
[video1]: https://youtu.be/V0wmD_y03iM?si=zY-5Qr7rLg5t0f8P
[video2]: https://www.youtube.com/watch?v=I-ohlZXXaxs&list=TLPQMjMwMTIwMjWqGEnALrOmfQ&index=6
[pubsub]: https://redis.io/docs/latest/develop/interact/pubsub/
[video3]: https://youtu.be/KIFA_fFzSbo?si=J_RwK3VIplYTOfL7
[video4]: https://youtu.be/p8mK8GBCARE?si=TcRIplWkQxWzgUaD
[video5]: https://youtu.be/-a07Ief51H4?si=qpg-XPJfC0iClNFM
[video6]: https://youtu.be/N8BkmdZzxDg?si=75c_v_1vzsuxicdV
[video7]: https://www.youtube.com/watch?v=1pfvz24BAUs
[roadmap]: https://roadmap.sh/redis
[metacaractere]: https://github.com/pedcravo/Wiki/tree/main/Linux/MetaCaractere
[redisconfig]: https://www.geeksforgeeks.org/complete-tutorial-of-configuration-in-redis/
[rdp&aof]:https://dev.to/thehollidayinn/backing-up-and-restoring-redis-25e5