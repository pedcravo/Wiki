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

---

## 🧐 O que é Git e GitHub

**Git** é um sistema de controle de versão distribuído usado para rastrear alterações em arquivos e facilitar o trabalho em equipe.  
**GitHub** é uma plataforma para hospedagem de repositórios Git, colaboração em projetos e muito mais.

---

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
- Iniciar um repositório:
```bash
  git init
```
- Adicionar arquivos:
```bash
  git add <arquivo> ou git add
```
- Commitar mudanças: git commit -m "Mensagem do commit"
- Verificar o status: git status
- Ver o histórico: git log

### Trabalhando com Branches
- Criar uma branch: git branch nome-da-branch
- Trocar de branch: git checkout nome-da-branch
- Mesclar branches: git merge nome-da-branch

### Remoto
- Clonar um repositório: git clone <url>
- Enviar alterações: git push
- Atualizar repositório local: git pull

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

[**Guia do GitHub**](https://docs.github.com/pt)
