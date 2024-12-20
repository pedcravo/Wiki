# Git e GitHub

Nesta seção vamos falar sobre o git e github.
Qualquer duvida nos conceitos é só clicar em um dos links na seção [**Recursos Úteis**](#recursos-úteis).

O **git** é um sistema controle e versionamento de arquivos distribuído usado para rastrear alterações em arquivos e facilitar o trabalho em equipe. 

- salva cada commit apontando pro commit anteior
- cada commit tem uma chave hash auto-incremento, onde a hash do commit anterior é adicionada a hash do novo commit
- cada commit é uma snapshot do estado dos arquivos, tornando assim rápida a transição entre eles.
- cada commit é um patch que pode ser aplicado a qualquer commit para ir ao estado da snapshot

- um branch é um caminho diferente dos arquivos no main. Tem um conceito semelhante ao de multiverso, onde caso algo fosse feito de diferente em determinado momento do tempo uma série de eventos (neste caso commits) podem acontecer sem interferir na linha do tempo original (main ou master).
- no git, assim como outros sistemas de versionamento de arquivos, é possível unir duas branchs e seguir o mesmo caminho ou isola-las novamente, este processo é chamado de merge.
- o git usa um sistema de 3 chaves para dar merge nos branchs, onde o git compara as alterações feitas em ambas as branchs e no commit em comum entre elas. Em alguns casos é necessário fazer alterações de merge manualmente.

Os arquivos podem estar em vários estados no sistema do git, como podemos ver nesta imagem:

<img src="https://github.com/pedcravo/Wiki/blob/gitgithub_issue%233/Git%26Github/Git.png" width="600px">

## Recursos Úteis
[**Documentação Oficial do Git**](https://git-scm.com/doc)

[**Documentação Oficial do Git em PT-BR**](https://git-scm.com/book/pt-br/v2/Come%c3%a7ando-Sobre-Controle-de-Vers%c3%a3o)

[**Guia do GitHub**](https://docs.github.com/pt)

[**Vídeo sobre Git**](https://youtu.be/6Czd1Yetaac?si=H7eOSQlWhTSD0PfM)

[**Corte do .git/obj**](https://youtube.com/clip/UgkxdbdLysxqglFwcK8ahZSO3Gkp2QUFTBNI?si=tkoNDcxbL1lW9t_m)

[**Tags no git**](https://medium.com/rafaeltardivo/git-criando-tags-7c34ee6786be)

[**Renomear commit no git**](https://www.atlassian.com/git/tutorials/rewriting-history)

[**Ignorando arquivos de commit no git**](https://www.freecodecamp.org/portuguese/news/gitignore-explicado-o-que-e-o-gitignore-e-como-adiciona-lo-ao-seu-repositorio/)

[**Renomeando branch no git**](https://kinsta.com/pt/base-de-conhecimento/git-rename-branch/)