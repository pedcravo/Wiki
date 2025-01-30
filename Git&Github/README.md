# Git e Github
Nesta seção vamos falar sobre o git e github.
Qualquer duvida nos conceitos é só clicar em um dos links na seção [**Recursos Úteis**](#recursos-úteis).

## Tópicos
- [Git e Github](#git-e-github)
  - [Tópicos](#tópicos)
  - [Conceitos](#conceitos)
  - [Conexão Remota com o Github](#conexão-remota-com-o-github)
  - [Fluxos de trabalho](#fluxos-de-trabalho)
    - [Local](#local)
      - [Para iniciar um projeto](#para-iniciar-um-projeto)
      - [Criar branchs](#criar-branchs)
      - [Deletar branchs](#deletar-branchs)
      - [Unir branchs](#unir-branchs)
      - [Navegar entre commits com branch](#navegar-entre-commits-com-branch)
      - [Commits](#commits)
      - [Revertendo Commits](#revertendo-commits)
      - [Resetando Commits Locais](#resetando-commits-locais)
      - [Diferenciando Commits (diff)](#diferenciando-commits-diff)
    - [Remoto](#remoto)
      - [Iníciar um projeto](#iníciar-um-projeto)
      - [Criar branch remota com base em uma local](#criar-branch-remota-com-base-em-uma-local)
      - [Importar branch remota para local](#importar-branch-remota-para-local)
      - [Conectar branch remota com uma local](#conectar-branch-remota-com-uma-local)
      - [Branchs remotas](#branchs-remotas)
      - [Renomear branchs](#renomear-branchs)
      - [Deletando branchs](#deletando-branchs)
      - [Unir branchs](#unir-branchs-1)
      - [Navegar entre commits com branch](#navegar-entre-commits-com-branch-1)
      - [Commits e atualizar remoto](#commits-e-atualizar-remoto)
      - [Revertendo Commits Remotos](#revertendo-commits-remotos)
      - [Resetando Commits Remotos](#resetando-commits-remotos)
      - [Diferenciando Commits (diff)](#diferenciando-commits-diff-1)
      - [Issues](#issues)
  - [Configurações globais](#configurações-globais)
  - [Recursos Úteis](#recursos-úteis)

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
Ao desenvolver localmente os arquivos serão mantidos na própia máquina.

#### Para iniciar um projeto 
1. Crie um diretório para o projeto:
    ```
    mkdir repository
    cd repository
    ```
2. Inicie um projeto git com o comando:
    ```
    git init
    ```

#### Criar branchs
Ao iniciar o projeto é criada uma branch principal. É possível criar outras branchs para trabalhar de forma mais organizada.

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

> **Criar branch e troca para ela:**
>   ```
>   git checkout -b <nome> <hash>
>   ```

O projeto foi íniciado, agora é possível **inserir arquivos a branch atual** do projeto.

#### Deletar branchs
O Git não permitirá que você exclua a ramificação em que você está atualmente, portanto, deve certificar-se de fazer o `checkout` de uma ramificação que você não está excluindo.
Logo siga essa série de comandos:

1. Troque para main ou outra branch diferente daquela que ira ser apagada:
   ```bash
   git checkout main
   ```
2. Apague a branch local:
   ```bash
   git branch -d <nome>.
   ```

> **OBS:**
> 
> A opção `-d` excluirá a ramificação somente se ela já tiver dado `push` ou `merge` com a branch remota. Use `-D` em vez disso, se você quiser forçar o ramo a ser excluído, mesmo que ele ainda não tenha dado `push` ou `merge`.

#### Unir branchs
Para unir duar branchs executamos o comando merge. Este comando faz um commit que tem como pais o ultimo commit de uma branch b1 e o ultimo commit de b2.

1. Vá para a branch **b1** (que vai ser "principal" na união) e atualize-a:
    ```bash
    git checkout b1
    ```
2. Faça merge de **b2** em * *b1**:
    ```bash
    git merge b2
    ```
3. Caso ocorra algum conflito entre branchs:
    - verifique quais arquivos estão em conflito.
    - edite os arquivos em conflito.
    - faça commit das alterações.

#### Navegar entre commits com branch
É possível modificar o local da branch em relação aos commits, ir adiante ou atrás do commit escolhido para iniciar a branch.

- Para ir para algum **commit em específico** utilize a hash dele para complementar o comando:
    ```bash
    git reset --hard <hash>
    ```
- Para ir até um **commit atrás do atual** utilize:
    ```bash
    git reset --hard HEAD^
    ```
- Para ir para um **commit onde outra branch está posicionada** utilize:
    ```bash
    git reset --hard <branch>
    ```

#### Commits
1. Criar ou editar arquivos no diretório do projeto.
2. Adiciona-los a área do stage:
    ```bash
    git add <arquivo>
        ou
    git add *
    ```
3. Verificar área de stage:
    ```bash
    git status
    ```
4. Enviar commit para a branch:
    ```bash
    git commit -am "Descrição do commit"
    ```
5. Ver total de commits:
    ```bash
    git log
        ou
    git log --oneline --graph --all
        ou
    gitk
    ```
---

#### Revertendo Commits
O comando `git revert <commit>` é usado para desfazer as alterações de um commit específico, criando um novo commit que reverte essas mudanças sem alterar o histórico do repositório.

- É necessário identificar o hash do commit que deseja reverter:
    ```bash
    git log --oneline
    ```

| Comando                                    | O que faz?                                                                                |
| :----------------------------------------- | :---------------------------------------------------------------------------------------- |
| `git revert <hash_do_commit>`              | Reverte um commit específico (abre um editor para inserir mensagem do commit)             |
| `git revert <hash_inicial>^..<hash_final>` | Reverte varios commits ao mesmo tempo                                                     |
| `git revert -n <hash_do_commit>`           | Reverte commit específico sem confirmação (precisará de commit para confirmar alterações) |

---
#### Resetando Commits Locais
O comando `git reset` é usado para desfazer alterações em commits locais. Ele pode modificar o histórico da branch, então deve ser usado com cautela.

- É necessário identificar o hash do commit que deseja reverter:
    ```bash
    git log --oneline
    ```

| Comando                    | O que faz?                                                                    |
| :------------------------- | :---------------------------------------------------------------------------- |
| `git reset --soft <hash>`  | Mantém as alterações dos commits resetados na área de stage                   |
| `git reset --mixed <hash>` | Mantém as alterações dos commits resetados no diretório de trabalho           |
| `git reset --hard <hash>`  | Remove completamente os commits e suas alterações (essa ação é irreversível!) |

---
#### Diferenciando Commits (diff)
Ainda é possível **ter uma visão das mudanças feitas nos arquivos do projeto**:

- Mostra mudanças entre o arquivo na aréa de edição e do stage:
    ```bash
    git diff
    ```
- Mostra mudanças entre o arquivo na areá do stage e o ultimo commit:
    ```bash
    git diff --staged
    ```


### Remoto
Caso você opte por manter seus arquivos remotamente, sua máquina irá ter uma cópia dos arquivos enquanto o servidor vai ter a principal. Será possível acessar de qualquer lugar os arquivos que estão na nuvem, porém sempre será necessário fazer o upload dos arquivos.

#### Iníciar um projeto
1. De inicio precisamos criar um projeto no Github.
2. Ir até a opção **"Code > Local > SSH"** e copiar o link.
3. Baixar o projeto remoto no git local para trabalhar no projeto:
    ```
    git clone -o <projeto> <ssh>
    ```

Por padrão é baixada a branch principal. Neste fluxo de trabalho **é possível iniciar branchs de formas diferentes**:

#### Criar branch remota com base em uma local
1. Criar branch local no commit da hash (caso não inserida, é criada no commit atual):
    ```bash
    git branch <nome> <hash>
    ```
2. Ver as branchs locais criadas e conectadas remotamente:
    ```bash
    git branch -vv
    ```
3. Entrar na branch criada:
    ```bash
    git checkout <nome>
    ```

> **Criar branch e troca para ela:**
>   ```bash
>   git checkout -b <nome> <hash>
>   ```

4. Criar branch remota conectada a local:
    ```bash
    git push -u <remota> <nome>
    ```

#### Importar branch remota para local
1. Criar a branch no github.
2. Importar branch para local:
    ```bash
    git checkout --track <remota>/<nome>
    ```

#### Conectar branch remota com uma local
1. Criar a branch no github.
2. Criar branch local no commit da hash (caso não inserida, é criada no commit atual):
    ```bash
    git branch <nome> <hash>
    ```
3. Ver as branchs locais criadas e conectadas remotamente:
    ```bash
    git branch -vv
    ```
4. Entrar na branch criada:
    ```bash
    git checkout <nome>
    ```
5. Conectar branch local com remota:
    ```bash
    git branch -u <remota>/<nome>
    ```

#### Branchs remotas
Podemos resumir os comandos para branchs no git em forma de tabela.
| Comandos           | Existe local? | Existe remoto? |
| :----------------- | :-----------: | :------------: |
| `push -u`          |     **V**     |     **X**      |
| `checkout --track` |     **X**     |     **V**      |
| `branch -u`        |     **V**     |     **V**      |

#### Renomear branchs
[**Renomeando branch no git**][Renomeando branch no git]]

[**Renomeando branchs no github**][Renomeando branchs no github]

#### Deletando branchs
O Git não permitirá que você exclua a ramificação em que você está atualmente, portanto, deve certificar-se de fazer o `checkout` de uma ramificação que você não está excluindo.
Logo siga essa série de comandos:

1. Troque para main ou outra branch diferente daquela que ira ser apagada:
   ```bash
   git checkout main
   ```
2. Apague a branch local:
   ```bash
   git branch -d <nome>.
   ```

> **OBS:**
> 
> A opção `-d` excluirá a ramificação somente se ela já tiver dado `push` ou `merge` com a branch remota. Use `-D` em vez disso, se você quiser forçar o ramo a ser excluído, mesmo que ele ainda não tenha dado `push` ou `merge`.

3. Apague a branch remotamente:
   ```bash
   git push <remota> --delete <nome>.
   ```

> Você também pode usar este comando mais curto para excluir um branch remotamente: 
>   ```bash
>   git push "remote" :'branch
>   ```


#### Unir branchs
Para unir duar branchs executamos o comando merge. Este comando faz um commit que tem como pais o ultimo commit de uma branch b1 e o ultimo commit de b2.

1. Cheque se os branchs que serão unidos estão na máquina:
    ```bash
    git branch -vv
    ```
2. Troque para a branch **b2** e atualize-a de acordo com o servidor:
    ```bash
    git checkout b2
    git pull
    ```
3. Vá para a branch **b1** (que vai ser "principal" na união) e atualize-a:
    ```bash
    git checkout b1
    git pull
    ```
4. Faça merge de **b2** em **b1**:
    ```bash
    git merge b2
    ```
5. Caso ocorra algum conflito entre branchs:
    - verifique quais arquivos estão em conflito.
    - edite os arquivos em conflito.
    - faça commit das alterações.
6. Atualize o servidor:
    ```bash
    git push
    ```

#### Navegar entre commits com branch
É possível modificar o local da branch em relação aos commits, ir adiante ou atrás do commit escolhido para iniciar a branch.
Lembre-se de sempre dar `git pull` antes e `git push` após executar o comando para atualizar o remoto.

- Para ir para algum **commit em específico** utilize a hash dele para complementar o comando:
    ```bash
    git reset --hard <hash>
    ```
- Para ir até um **commit atrás do atual** utilize:
    ```bash
    git reset --hard HEAD^
    ```
- Para ir para um **commit onde outra branch está posicionada** utilize:
    ```bash
    git reset --hard <branch>
    ```

#### Commits e atualizar remoto
Agora **para inserir arquivos na branch** atual do projeto, o caminho é muito semelhante ao feito no outro fluxo.
1. Recuperar dados da branch no servidor e uni-los com os da máquina:
    ```bash
    git pull
    ```
2. Criar ou editar arquivos no diretório local do projeto.
3. Adiciona-los a área do stage:
    ```bash
    git add <arquivo>
        ou
    git add *
    ```
4. Verificar área de stage:
    ```bash
    git status
    ```
5. Enviar commit para a branch:
    ```bash
    git commit -am "Descrição do commit"
    ```
6. Ver total de commits e onde está projeto local em relação ao remoto:
    ```bash
    git log
        ou
    git log --oneline --graph --all
        ou
    gitk
    ```
7. Enviar mudanças feitar ao servidor:
    ```bash
    git push
    ```

#### Revertendo Commits Remotos
Quando um commit já foi enviado para o repositório remoto e precisa ser revertido, o `git revert` pode ser usado para criar um novo commit que desfaz as alterações, mantendo o histórico intacto.
Os comandos são semelhantes porém por fim é necessário enviar as alterações para o remoto atráves do `git push`.

- É necessário identificar o hash do commit que deseja reverter:
    ```bash
    git log --oneline
    ```

| Comando                                    | O que faz?                                                                                |
| :----------------------------------------- | :---------------------------------------------------------------------------------------- |
| `git revert <hash_do_commit>`              | Reverte um commit específico (abre um editor para inserir mensagem do commit)             |
| `git revert <hash_inicial>^..<hash_final>` | Reverte varios commits ao mesmo tempo                                                     |
| `git revert -n <hash_do_commit>`           | Reverte commit específico sem confirmação (precisará de commit para confirmar alterações) |

Por fim é necessário enviar alterações ao servidor:
```bash
git push
```

---
#### Resetando Commits Remotos
Quando um commit já foi enviado para o repositório remoto, o `git reset` pode ser usado para reescrever o histórico local, mas será necessário forçar a atualização no remoto com `git push --force`.

> **Atenção:** Usar `git push --force` pode causar perda de histórico e problemas ao trabalhar em equipe.

- É necessário identificar o hash do commit que deseja reverter:
    ```bash
    git log --oneline
    ```

| Comando                                    | O que faz?                                                                                |
| :----------------------------------------- | :---------------------------------------------------------------------------------------- |
| `git revert <hash_do_commit>`              | Reverte um commit específico (abre um editor para inserir mensagem do commit)             |
| `git revert <hash_inicial>^..<hash_final>` | Reverte varios commits ao mesmo tempo                                                     |
| `git revert -n <hash_do_commit>`           | Reverte commit específico sem confirmação (precisará de commit para confirmar alterações) |

Enviar as alterações ao servidor (com cuidado!):
```bash
git push --force
```


---
#### Diferenciando Commits (diff)
Assim como no local, é possível **ter uma visão das mudanças feitas nos arquivos do projeto**:

- Mostra mudanças entre o arquivo na aréa de edição e do stage:
    ```bash
    git diff
    ```
- Mostra mudanças entre o arquivo na areá do stage e o último commit:
    ```bash
    git diff --staged
    ```

#### Issues
Ao trabalhar remotamente no git é muito comum o uso de issues. Para inserir um commit a uma issue é necessário utilizar o **#n** (sendo **n** o número da issue), este commit ao ser enviado para o servidor vai automáticamente para a issue.
    ```bash
    git commit -am "Este commit vai para a issue (#3)"
    ```

## Configurações globais
No git é possível definir configurações globais, padronizando assim todos os projetos sequentes ou atuais (dependendo das alterações). Para isso é necessário editar o arquivo `.gitconfig` do usuário.

Podemos citar algumas configurações globais uteis a serem feitas como:
- **Usuário:** Define o usuário padrão e  o email que vai ser usado na assinatura (geralmente os mesmos do Github).
```bash
[user]
        name = Pedro Cravo
        email = pedroh.s.cravo@gmail.com
```

- **Core:** Define configurações básicas ao git como qual o editor de texto padrão do sistema e qual o arquivo padrão para arquivos ignorados ao fazer `git add *`.
```bash
[core]
        editor = nano
        excludesfile = /home/pedro/.gitignore_global
```

- **Init:** Definque qual a branch padrão ao iniciar um projeto.
```bash
[init]
        defaultBranch = main
```

- **Color:** Define a detecção de espaços em branco e diffs coloridos.
```bash
[color]
        ui = auto
```

- **Alias:** Define aliases para comandos `git`.
``` bash
[alias]
        br = branch
        co = checkout
        lg = log --oneline --graph --all
        st = status
        ad = add *
        cm = commit -am
        ps = push
        pl = pull
```


## Recursos Úteis
[**Documentação Oficial do Git**](https://git-scm.com/doc)

[**Documentação Oficial do Git em PT-BR**](https://git-scm.com/book/pt-br/v2/Come%c3%a7ando-Sobre-Controle-de-Vers%c3%a3o)

[**Roadmap GIt e Github**](https://roadmap.sh/git-github)

[**Livro Git and Github**](https://books.goalkicker.com/GitBook/)

[**Guia do GitHub**](https://docs.github.com/pt)

[**Vídeo sobre Git**](https://youtu.be/6Czd1Yetaac?si=H7eOSQlWhTSD0PfM)

[**Tags no git**](https://medium.com/rafaeltardivo/git-criando-tags-7c34ee6786be)

[**Renomear commit no git**](https://www.atlassian.com/git/tutorials/rewriting-history)

[**Ignorando arquivos de commit no git**](https://www.freecodecamp.org/portuguese/news/gitignore-explicado-o-que-e-o-gitignore-e-como-adiciona-lo-ao-seu-repositorio/)

[**Renomeando branch no git**][Renomeando branch no git]]

[**Renomeando branchs no github**][Renomeando branchs no github]

[Renomeando branch no git]: https://kinsta.com/pt/base-de-conhecimento/git-rename-branch/
[Renomeando branchs no github]: https://docs.github.com/pt/repositories/configuring-branches-and-merges-in-your-repository/managing-branches-in-your-repository/renaming-a-branch