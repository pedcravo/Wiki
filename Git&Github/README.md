# 🚀 Git e GitHub

Bem-vindo ao meu guia pessoal sobre Git e GitHub! Este repositório é um espaço para organizar e compartilhar meus estudos, anotações e exemplos práticos relacionados ao controle de versão e colaboração com Git e GitHub.

---

## 📚 Índice

1. [O que é Git e GitHub](#o-que-é-git-e-github)
2. [Configuração Inicial](#configuração-inicial)
3. [Principais Comandos do Git](#principais-comandos-do-git)
4. [Fluxos de Trabalho com GitHub](#fluxos-de-trabalho-com-github)
5. [Boas Práticas](#boas-práticas)
6. [Problemas Comuns e Soluções](#problemas-comuns-e-soluções)
7. [Recursos Úteis](#recursos-úteis)


## 🧐 O que é Git e GitHub

**Git** é um sistema de controle de versão distribuído usado para rastrear alterações em arquivos e facilitar o trabalho em equipe. Criado em 2005 por Linus Torvalds.

**GitHub** é uma plataforma para hospedagem de repositórios Git, colaboração em projetos e muito mais.

**Commit** é um registro de alterações feitas em um projeto, que captura o estado dos arquivos em um determinado momento. É um **patch** de alterações desde o **commit** anterior. Cada **commit** aponta para o **commit** anterior.

**Master** é o projeto principal, o conjunto principal de **commits** do projeto, base dos **branchs**.

**Branch** é uma cópia de algum momento do projeto separada para o desenvolvedor sem interferir no **master**. Internamente é uma cópia do master que 

**Patch** é um arquivo que tem as alterações feitas no arquivo da versão anterior para a nova versão, é usado para carregar as alterações de um projeto. Ele é criado com base no diff. Cada patch tem um **hash (SHA-1)** que é a assinatura daquele delta, o hash é a prova que o patch está correto.

**Diff** é um comando do Git que compara fontes de dados, como arquivos, commits, ramificações, e dá origem ao patch.


Merge

Subscripcion 

Para mais informações acesse: [**Vídeo de Git**](https://youtu.be/6Czd1Yetaac?si=H7eOSQlWhTSD0PfM)


## 🔧 Configuração Inicial

### Instalação do Git
```Bash
  apt install git
```
Instala git e suas dependências.

Para mais informações acesse: [Guia oficial de instalação](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

### Configuração Básica
```bash
git config --global user.name "Seu Nome"
git config --global user.email "seuemail@example.com"
```


## 🛠️ Principais Comandos do Git
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

### Remoto
- Clonar/puxar um repositório para sua máquina: `git clone <url>`
- Enviar alterações: `git push`
- Atualizar repositório local: `git pull`

      git cat-file -p HEAD
      git cat-file -p HEAD^{tree}
      git cat-file -p f21dc2804e888fee6014d7e5b1ceee533b222c15
      git cat-file -p master
Mostram os hashs dos arquivos dos diretórios e das trees.

      git tag
Mostra as versões.

      git cat-file -p v1.0
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

[**Vídeo de Git**](https://youtu.be/6Czd1Yetaac?si=H7eOSQlWhTSD0PfM)



[**Corte do .git/obj**](https://youtube.com/clip/UgkxdbdLysxqglFwcK8ahZSO3Gkp2QUFTBNI?si=tkoNDcxbL1lW9t_m)
