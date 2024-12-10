# 🚀 Git e GitHub

Bem-vindo ao meu guia pessoal sobre Git e GitHub! Este repositório é um espaço para organizar e compartilhar meus estudos, anotações e exemplos práticos relacionados ao controle de versão e colaboração com Git e GitHub.


## 📚 Índice

1. [O que é Git e GitHub](##-o-que-é-git-e-github)
2. [Configuração Inicial](#configuração-inicial)
3. [Principais Comandos do Git](#principais-comandos-do-git)
4. [Fluxos de Trabalho com GitHub](#fluxos-de-trabalho-com-github)
5. [Boas Práticas](#boas-práticas)
6. [Problemas Comuns e Soluções](#problemas-comuns-e-soluções)
7. [Recursos Úteis](#-recursos-úteis)


## 🧐 O que é Git e GitHub

- **Git** é um sistema de controle de versão distribuído usado para rastrear alterações em arquivos e facilitar o trabalho em equipe. Criado em 2005 por Linus Torvalds.

**GitHub** é uma plataforma para hospedagem de repositórios Git, colaboração em projetos e muito mais.

**Master** é o projeto original, o conjunto principal de **commits** do projeto, base dos **branchs**.

**Branch** é uma cópia de algum momento do projeto separada para o desenvolvedor sem interferir no **master**. Internamente é uma cópia do **master** que ainda aponta para o **commit** anterior a ela.

**Commit** é um registro de alterações feitas em um projeto que captura o estado dos arquivos em um determinado momento. É um **patch** de alterações desde o **commit** anterior, aponta para o **commit** anterior.

**Patch** é um arquivo que tem as alterações feitas no projeto desde a versão anterior, é usado para carregar as alterações do projeto. Cada **patch** tem um **hash (SHA-1)** que é a assinatura daquele delta, o **hash** é a prova que o **patch** está correto.

**Diff** é um comando do Git que compara fontes de dados, como arquivos, commits e ramificações que dá origem ao **patch**.

**Merge** é a união do **branch** com o **master**. Internamente é como dar um **diff** na **branch** e usar os **patch**s de cada arquivo resultante para atualizar (dar **commit**) o **master**.
Em casos de dois ou mais **branchs** o Git compara os **branchs** com o **master** de origem e escolhe a versão modificada mais recente para permanecer, em seguida cria um **commit** de **branch** que torna este o **master** de origem.

Para mais informações veja o vídeo: [**Vídeo sobre Git**](https://youtu.be/6Czd1Yetaac?si=H7eOSQlWhTSD0PfM)


## 🔧 Configuração Inicial

### Instalação do Git
Para instalar o git e suas dependencias use o comando:
~~~bash
  $ apt install git
~~~

Para mais informações acesse: [Guia oficial de instalação](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

### Configuração Básica
A primeira coisa que você deve fazer ao instalar Git é **configurar seu nome de usuário e endereço de e-mail**. Isto é importante porque cada commit usa esta informação, e ela é carimbada de forma imutável nos commits que você começa a criar:

~~~bash
  $ git config --global user.name "Seu Nome"
  $ git config --global user.email seuemail@example.com
~~~

Se você quiser substituir essa informação com nome diferente para um projeto específico, você pode rodar o comando sem a opção `--global` dentro daquele projeto.

Muitas ferramentas GUI o ajudarão com isso quando forem usadas pela primeira vez.

Você pode **escolher o editor de texto padrão** que será chamado quando Git precisar que você entre uma mensagem. Se não for configurado, o Git usará o editor padrão, que normalmente é o Vim. Se você quiser usar um editor de texto diferente, como o Emacs, você pode fazer o seguinte:
~~~bash
  $ git config --global core.editor <editor>
~~~

>**OBS:** Vim e Emacs são editores de texto populares comumente usados por desenvolvedores em sistemas baseados em Unix como Linux e Max. Se você não for acostumado com estes editores ou estiver em um sistema Windows, você precisará procurar por instruções de como configurar o seu editor preferido com Git. Se você não configurar o seu editor preferido e não sabe usar o Vim ou Emacs, é provável que você fique bastante confuso ao entrar neles.
Testando Suas Configurações

Também é interessante usar o comando para definir o nome da branch principal. Nomes comuns: 'master' are 'main', 'trunk' and hint: 'development'
~~~bash
  $ git config --global init.defaultBranch <nome>
~~~

Para renomear o branch use:
~~~bash
git branch -m <nome>
~~~

Se você quiser **testar as suas configurações**, você pode usar o comando `git config --list` para listar todas as configurações que o Git conseguir encontrar naquele momento:
~~~bash
  $ git config --list
~~~


## 🛠️ Principais Comandos do Git
### Pedindo ajuda
Há três formas de acessar a página do manual de ajuda (manpage) para qualquer um dos comandos Git:
~~~bash
  $ git help <verb>
  $ git <verb> --help
  $ man git-<verb>
~~~
Por exemplo, você pode ver a manpage do commando config rodando: `$ git help config`

### Iniciando um projeto Git
Você pode iniciar um projeto Git utilizando duas formas principais:
1. Usar como base um diretório local que atualmente não está sob controle de versão e transformá-lo em um repositório Git. Neste caso segue-se o **Fluxo Básico**.
2. Fazer um clone de um repositório Git existente em outro lugar. Neste caso segue-se o **Fluxo Remoto**.

Em vez de receber apenas uma cópia para trabalho, o Git recebe uma cópia completa de praticamente todos os dados que o servidor possui.



### Fluxo Básico
- Iniciar um repositório: `git init`
- Adicionar arquivos **(marcar alterações)**: `git add <arquivo> ou git add`
- Commitar mudanças: `git commit -m "Mensagem do commit"`
- Verificar o status: `git status`
- Ver o histórico: `git log`

### Trabalhando com Branches
- Criar uma branch: `git branch nome-da-branch`
- Trocar de branch: `git checkout nome-da-branch`
- Mesclar branches: `git merge nome-da-branch`

### Fluxo Remoto
- Clonar/puxar um repositório para sua máquina: `git clone <url>`
- Enviar alterações: `git push`
- Atualizar repositório local: `git pull`
~~~bash
  $ git cat-file -p HEAD
  $ git cat-file -p HEAD^{tree}
  $ git cat-file -p f21dc2804e888fee6014d7e5b1ceee533b222c15
  $ git cat-file -p master
~~~
Mostram os hashs dos arquivos dos diretórios e das trees.
~~~bash
  $ git tag
~~~
Mostra as versões.
~~~bash
  $ git cat-file -p v1.0
~~~
Mostra informações sobre o commit v1.0 


## 🌐 Fluxos de Trabalho com GitHub
- **Fork e Pull Request:** Para contribuir em repositórios de terceiros.
- **Issues e Discussions:** Gerenciando e discutindo tarefas.
- **Actions:** Automatizando fluxos de trabalho.

1. Executa um `git clone` no diretório que deseja;
2. Faz alterações no arquivo da máquina;
3. Executa `git add` para marcar as alterações;
4. Executa `git commit` para empacotar as alterações num **patch**;


## ✅ Boas Práticas
- Sempre escreva mensagens de commit **claras e descritivas**.
- **Use branches** para **organizar** funcionalidades e correções.
- Sincronize **frequentemente** seu repositório local com o remoto: ` git pull `
- Revise mudanças **antes de fazer o commit**.
- Resolva conflitos de merge com a**tenção e paciência**.

## 🛡️ Problemas Comuns e Soluções
- **Conflitos de Merge:** Como identificar e resolver conflitos.
- **Erro ao Clonar Repositório:** Checar URL e permissões.

## 🌟 Recursos Úteis
[**Documentação Oficial do Git**](https://git-scm.com/doc)

[**Documentação Oficial do Git em PT-BR**](https://git-scm.com/book/pt-br/v2/Come%c3%a7ando-Sobre-Controle-de-Vers%c3%a3o)

[**Guia do GitHub**](https://docs.github.com/pt)

[**Vídeo sobre Git**](https://youtu.be/6Czd1Yetaac?si=H7eOSQlWhTSD0PfM)

[**Corte do .git/obj**](https://youtube.com/clip/UgkxdbdLysxqglFwcK8ahZSO3Gkp2QUFTBNI?si=tkoNDcxbL1lW9t_m)
