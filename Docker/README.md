# Docker
Nesta seção veremos o que é docker, alguns conceitos relacionados a ele e comandos para interagir com o docker.

## Conceitos
**Docker** é uma plataforma de containerização que permite criar, gerenciar e executar **containers** de forma simples e eficiente. Ele proporciona ambientes isolados para aplicativos, garantindo consistência e portabilidade entre diferentes sistemas.

**Containers** são ambientes isolados de execução criados a partir de **imagens Docker**. Eles contêm tudo o que é necessário para rodar um aplicativo, incluindo bibliotecas, dependências e arquivos de configuração. Os containers tem como caracteristicas principais:
- Leves e rápidos;
- Compartilham o kernel do sistema operacional do host;
- Isolados entre si e do sistema host.

**Imagens** são templates estáticos usados para criar **containers**. Elas contêm o sistema operacional básico, bibliotecas, dependências e o aplicativo configurado para rodar. Tem como principais características:
- Imutáveis após sua criação;
- Reutilizáveis, sendo possível gerar vários containers a partir da mesma imagem;
- Versionadas com tags (ex.: nginx:alpine).

## Comandos para Gerenciamento de Containers
Ao gerenciar containers no docker é comum o uso da opção `container` após o comando `docker` indicando explicitamente que está interagindo com um container, porém o seu uso não é obrigatório para a maioria dos comandos pois o docker entende implissitamente que a interação está sendo feita com um container.

### Criar Container
A opção utilizada pelo docker para baixar, criar e rodar containers é `run` ou algum de seus **aliases** (`docker container run`, `docker run`), como pode ser visto neste comando base:
```bash
docker container run [OPÇÕES] IMAGEM [COMANDO] [ARG...]
```

Essa é um comando base para instalar uma **imagem docker** e torna-la um **container**, podendo através de opções extras modificar caracteristicas do container. É possível passar comandos para serem executados após a instalação do container como um simples `echo "Hello World"`.

> Caso a versão da **imagem** não seja definida, o docker vai instalar a ultima versão ou *latest*.

A forma mais comum ao instalar um container é 
```bash
docker run -it IMAGEM
```

#### Opções úteis:
|Opção|Uso|
|:----|:--|
|`-d`| Usado para executar o container em segundo plano, torna semelhante a um daemon|
|`-e` `--env`| Define uma variavel global|
|`-i` | Torna a instalação interativa|
|`--name`| Utilizado para dar um nome personalizado ao container|
|`-p`| Mapeia portas (ex.: -p 8080:80)|
|`-q`| Torna a instalação silenciosa, não mostra nada na tela|
|`--rm`| Remove automaticamente o container após parar|
|`-t`| Abre o terminal do container|


### Executar comandos em Container
Para executar comandos dentro de containers é usada a opção `exec` ou algum de seus **aliases** (`docker container exec`, `docker exec`), como podemos ver neste comando base:
```bash
docker container [OPÇÔES] exec CONTAINER COMANDO
```

A forma mais comum da opção `exec` é a seguinte:
```bash
docker exec -it CONTAINER COMANDO
```

#### Opções úteis:
|Opção|Uso|
|:----|:--|
|`-d`| Usado para executar o container em segundo plano, torna semelhante a um daemon|
|`-e` `--env`| Define uma variavel global|
|`-i` | Torna a instalação interativa|
|`-t`| Abre o terminal do container|


### Excluir Container
Para excluir containers é utilizada a opção `rm` ou algum de seus **aliases** (`docker container rm`, `docker container remove`, `docker rm`), como é possível ver neste comando base:
```bash
docker container rm [OPÇÕES] CONTAINER [CONTAINER...]
```

A forma mais comum para remover um container:
```bash
docker rm -f CONTAINER
```
A opção `-f` é utilizada para forçar o container a ser apagado.


### Para e Iniciar Container
Ao baixar um container é possivel para-lo ou inicia-lo.

Para parar um container:
```bash
docker container stop CONTAINER
```

Para iniciar um container:
```bash
docker container start CONTAINER
```

### Mostrar Containers
Para o mostrar os containers presentes no docker a opção utilizada é `ps` ou algum de seus **aliases** (`docker container ls`, `docker container list`, `docker container ps`, `docker ps`), como podemos ver neste comando base:
```bash
docker container ps [OPÇÕES]
```

A forma mais comum do uso desta opção é:
```bash
docker ps -al
```

Outra forma comum deste comando com formatação da saída:
```bash
docker ps -al --format "table {{.Names}}\t{{.Image}}\t{{.Status}}"
```

#### Opções úteis:
|Opção|Uso|
|:----|:--|
|`-a`| Mostra todos|
|`-f`| Filtra os containers mostrados|
|`--format`| Formata a saída do comando|
|`-n` | Mostra o s ultimos **n** containers|
|`-l`| Mostra o ultimo container|
|`-q`| Mostra apenas os ids dos containers|


### Mostrar logs de Container
Para mostrar os logs de um container é utilizada a opção `logs` ou algum de seus **aliasses** (`docker container logs`, `docker logs`), como é possível ver a seguir:
```bash
docker container logs CONTAINER
```

Uma das formas mais utilizadas é:
```
docker logs -n 10 CONTAINER
```

#### Opções úteis:
|Opção|Uso|
|:----|:--|
|`-f`| Segue os logs em tempo real|
|`-n`| Mostra o s ultimos **n** containers|
|`-t`| Mostra os logs em determinado período de tempo|