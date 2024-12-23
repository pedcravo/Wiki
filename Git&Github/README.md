# Git e GitHub

Nesta seção vamos falar sobre o git e github.
Qualquer duvida nos conceitos é só clicar em um dos links na seção [**Recursos Úteis**](#recursos-úteis).


## Conceitos
O **Git** é um sistema controle e versionamento de arquivos distribuído usado para rastrear alterações em arquivos e facilitar o trabalho em equipe.

**Commit** é um registro de alterações feitas em um projeto que captura o estado dos arquivos em um determinado momento (snapshot). **Cada commit tem uma chave hash** auto-incremento, onde a hash do commit anterior é adicionada a hash do novo commit, tornando assim cada novo commit um ponteiro para o commit anterior. Os commits se assemelham com uma lista encadeada, onde **cada um aponta para o seu anterior**.
Enquanto registro das alterações dos arquivos tem a funçõe de patch do projeto, que pode ser aplicado a qualquer commit para muda-lo para o estado da snapshot tornando assim rápida a transição entre commits.

**Branch** é um caminho diferente que os arquivos do projeto podem tomar além do main. Tem um conceito semelhante ao de multiverso, onde caso algo fosse feito de diferente em determinado momento do tempo uma série de eventos (neste caso commits) podem acontecer sem interferir na linha do tempo original (main ou master).

No git, assim como outros sistemas de versionamento de arquivos, é possível unir duas branchs e seguir o mesmo caminho ou isola-las novamente, este processo é chamado de **merge**. É usado um sistema de **3 chaves** para dar merge nos branchs, onde o git compara as alterações feitas em ambas as branchs e no commit em comum entre elas. Em alguns casos é necessário fazer alterações de merge manualmente.

Os arquivos podem estar em vários estados no sistema do git, como podemos ver nesta imagem:

<img src="https://github.com/pedcravo/Wiki/blob/gitgithub_issue%233/Git%26Github/Git.png" width="600px">

> No git é possível desenvolver localmente e manter os arquivos salvos localmente bem como envia-los a nuvem, para isso temos o github (mais famoso na área).

O **Github** é uma plataforma de hospedagem de repositórios git, colaboração em projetos e muito mais.É possível fazer conexões remotas de diversas maneiras com esta plataforma, mas iremos abordar apenas a conexão via ssh que é a mais comum e segura.

## Conexão Remota com o Github

Caso não tenha e queira gerar chave ssh siga os seguintes passos:
1. Usar o comando **`ssh-keygen -t rsa`** para criar uma chave ssh na máquina local.
2. Inserir uma senha forte.
3. Ir para `~/.ssh` e checar os arquivos `id_rsa` e `id_rsa.pub`.

Para conectar via ssh no github siga os seguintes passos:
1. Ir para `~/.ssh` e checar os arquivos `id_rsa` e `id_rsa.pub`.
2. Copiar todo conteúdo do arquivo `id_rsa.pub`.
3. Acessar seu perfil no **Github > Settings > "SSH and GPG Keys"**
4. Clicar em **"New SSH Key"**.
5. Inserir um título e colar o conteúdo de `id_rsa.pub` no campo **"Key"**.

## Fluxos de trabalho
Como já foi dito, é possível seguir dois caminhos diferentes de trabalho no git sendo o fluxo local e o remoto. 

### Local
Ao desenvolver localmente os arquivos serão mantidos na própia máquina. **Para iniciar e desenvolver** um projeto git local:

1. Crie um diretório para o projeto:
    ```
    mkdir repository
    cd /home/user/repository
    ```
2. Inicie um projeto git com o comando:
    ```
    git init
    ```

Ao iniciar o projeto é criada uma branch principal. **Para criar outras branchs**:

1. Criar branch no commit da hash (caso não inserida, é criada no commit atual):
    ```
    git branch <nome> <hash>
    ```
2. Ver as branchs criadas:
    ```
    git branch
    ```
3. Entrar na branch criada:
    ```
    git checkout <nome>
    ```

> Criar branch e troca para ela:
>   ```
>   git checkout -b <nome> <hash>
>   ```

O projeto foi íniciado, agora é possível **inserir arquivos a branch atual** do projeto:

1. Criar e editar arquivos no diretório do projeto.
2. Adiciona-los a área do stage:
    ```
    git add <arquivo>
        ou
    git add *
    ```
3. Enviar commit para a branch:
    ```
    git commit -am "Descrição do commit"
    ```
4. Ver total de commits:
    ```
    git log
        ou
    git log --oneline --graph --all
    ```

### Remoto
Caso você opte por manter seus arquivos remotamente, sua máquina irá ter uma cópia dos arquivos enquanto o servidor vai ter a principal. Será possível acessar de qualquer lugar os arquivos que estão na nuvem, porém sempre será necessário fazer o upload dos arquivos.

Neste fluxo de trabalho é possível iniciar de formas diferentes:
#### Criar o projeto remoto e importando-o com link para sua máquina:
1. De inicio precisamos criar um projeto no Github;
2. Ir até a opção **"Code > Local > SSH"** e copiar o link.

    ```Bash
    git
    ```

#### Criar o projeto remoto e conectando em um projeto já existente na máquina: 
Onde o inicio a criação do projeto é semelhante ao fluxo local, porém o diferencial é a conexão dele com o remoto.

Criação de branchs

## Recursos Úteis
[**Documentação Oficial do Git**](https://git-scm.com/doc)

[**Documentação Oficial do Git em PT-BR**](https://git-scm.com/book/pt-br/v2/Come%c3%a7ando-Sobre-Controle-de-Vers%c3%a3o)

[**Guia do GitHub**](https://docs.github.com/pt)

[**Vídeo sobre Git**](https://youtu.be/6Czd1Yetaac?si=H7eOSQlWhTSD0PfM)

[**Tags no git**](https://medium.com/rafaeltardivo/git-criando-tags-7c34ee6786be)

[**Renomear commit no git**](https://www.atlassian.com/git/tutorials/rewriting-history)

[**Ignorando arquivos de commit no git**](https://www.freecodecamp.org/portuguese/news/gitignore-explicado-o-que-e-o-gitignore-e-como-adiciona-lo-ao-seu-repositorio/)

[**Renomeando branch no git**](https://kinsta.com/pt/base-de-conhecimento/git-rename-branch/)