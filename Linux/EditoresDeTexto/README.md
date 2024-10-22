# Editores de Texto no Linux

Nesta seção, exploramos comandos relacionados à execução e manipulação de shells no Linux, incluindo o Bash, que é o shell padrão em muitas distribuições.
O Bash permite executar scripts, iniciar sessões de shell e manipular variáveis de ambiente, sendo uma ferramenta fundamental para automação e controle de processos no Linux.

### Comandos:

1. [`bash`](#1-bash)
2. [`Nano`](#2-nano)
3. [`sed`](#3-sed)
4. [`vi`](#4-vi)

---

## 1. `bash`

### Para que serve?
O comando `bash` pode ser usado para **iniciar uma nova sessão de shell, executar scripts de shell, ou executar comandos interativamente**. O `bash` é o shell padrão em muitas distribuições Linux e permite automação, controle de processos, e manipulação de arquivos.

O comando bash também pode ser usado para depurar scripts e gerenciar variáveis de ambiente e execução de comandos.

#### Arquivos de configuração:
- `/etc/profile`: Contém configurações globais que afetam todos os usuários.
- `~/.bashrc`: Contém configurações específicas do usuário para o Bash interativo.
- `~/.bash_profile`: Carregado no login de um shell Bash.

### Opções:
- `-c` → Executa um comando ou conjunto de comandos fornecidos entre aspas, sem iniciar um novo shell interativo.
- `-i` → Inicia uma nova sessão interativa do `bash`. Mesmo que seja fornecido um comando, o `bash` aguarda a entrada de comandos diretamente do usuário.
- `-l` → Inicia o shell como login shell, carregando as configurações de ambiente, como o `/etc/profile` e `~/.bash_profile`.
- `-v` → Executa o script em modo verbose. Mostra o script linha por linha conforme ele é executado.
- `-x` → Executa o script com depuração, exibindo cada comando antes de ser executado.

### Sintaxe comum:
**`$ bash [OPÇÕES] COMANDO/ARQUIVO`**

### Exemplos:
`$ bash script.sh` → Roda o script usando o `bash`.

`$ bash -c ‘ls -l /home’` → Executa o comando `ls -l /home` sem abrir uma nova sessão interativa.

`$ bash -x script.sh` → Executa script.sh com depuração, mostrando cada comando antes de ser executado.

`$ bash --version` → mostra qual a versão do `bash`.

### Máterial Complementar:
Não possui material complementar.

---

## 2. `Nano`

### Para que serve?
É um editor de texto, muito simples e fácil de utilizar, com diversos comandos e atalhos.
**Caso o arquivo que deseja abrir não exista, ele cria um novo (padrão linux).**
Sempre que salva pergunta qual será o nome do arquivo, se o arquivo tiver o nome modificado o original segue intacto (backup) enquanto o arquivo alterado é salvo com novo nome.

### Opções:
- `--help` → Vai para aba de ajuda.
- `-B` → Faz um backup do arquivo antes das mudanças.
- `-I` → Ativa a identação automática.
- `-N` → Não converte no formato DOS/Mac.
- `-T` → Define o tamanho de espaços ao utilizar `tab`.
- `-U` → Ativa as funcionalidades.
- `+N` → Abre o arquivo na linha `N`.
- `-c` → Mostra constantemente a posição do cursor.
- `-i` → Faz a identação automática em novas linhas.
- `-k` → Alternar cortar para que ele corte a partir da posição do cursor.
- `-m` → Liga o suporte ao mouse.
- `-v` → Abre o arquivo em modo view.

#### Comandos dentro do editor:
**Ctrl + g** → Aba de ajuda.

**Ctrl + x** → Salvar e sair.

**Ctrl + o** → Salvar.

**Ctrl + s** → Salva para continuar trabalhando.

**Ctrl + w** → Pesquisar no arquivo.

**Ctrl + a** → Leva o cursor ao inicio da linha.

**Ctrl + e** → Leva o cursor ao fim da linha.

**Ctrl + r** → Insere outro arquivo dentro do arquivo atual.

**Ctrl + \\** → Substituir.

**Ctrl + k** → Recortar.

**Ctrl + u** → Colar.

**Ctrl + t** → Executar arquivo.

**Ctrl + c** → Mostra onde está o cursor, a linha em que ele está, caracteres que antes e depois, etc.

**Alt + g** → Escolher qual linha quer ir.

**Alt + \\** → Ir para o inicio do arquivo.

**Alt + /** → Ir para o fim do arquivo.

### Sintaxe comum:
**`$ nano [OPÇÕES] ARQUIVO`**

### Exemplos:
`$ nano arquivo.txt` → Abre o arquivo com editor de texto

`$ nano +3 arquivo.txt` → Abre o arquivo na 3ª linha

`$ nano -c arquivo.txt` → Abre o arquivo com editor de texto

### Máterial Complementar:
https://ioflood.com/blog/nano-linux-command/

https://forum.netgate.com/topic/50484/dica-instalar-editor-nano

https://www.nano-editor.org/

---

## 3. `sed` 

### Para que serve?
Utilizado para **manipular e editar textos em arquivos** de maneira eficiente e não interativa.

O `sed` (Stream Editor) pode realizar operações como **substituição, inserção, exclusão de texto**, e muitas outras transformações em um fluxo de dados.

Ele não altera o arquivo original a menos que seja usado com a opção -i (edição no local).

### Opções:
- `s/padrão/substituição/` → Substitui a primeira ocorrência do padrão especificado em cada linha.
- `s/padrão/substituição/g` → Substitui todas as ocorrências do padrão em cada linha (global).
- `/palavra/d` → Remove as linhas que tem a palavra.

- `Ni` → Antes da `N` linha (ou a ultima = `$`).
- `Na` → Após a `N` linha (ou a ultima = `$`).
- `d` → Deleta linhas que correspondem a um padrão.
- `p` → Exibe as linhas que correspondem ao padrão.
- `-n` → Suprime a saída padrão, útil em combinação com p para exibir somente o que foi solicitado.
- `-e` → Permite adicionar múltiplas expressões.
- `-f` → Script file sed para escrever expressões sed em outro arquivo.
- `-i` → Faz a edição diretamente no arquivo, sem exibir a saída no terminal.
- `-i .bak` → Faz a edição diretamente no arquivo e cria um arquivo backup (`.bak`).
- `-r` → Habilita a utilização de expressões regulares estendidas.

### Sintaxe comum:
**`$ sed [OPÇÕES] TROCA ARQUIVO`**

### Exemplos:
`$ sed 's/antigo/novo/' arquivo.txt` → Substitui a primeira ocorrência da palavra "antigo" por "novo" em cada linha do arquivo e mostra na tela.

$ sed 's/antigo/novo/g' arquivo.txt → substitui ocorrência da palavra "antigo" por "novo" em cada linha do arquivo e mostra na tela
$ sed '/root/s:/bin/bash:/bin/false:' /etc/passwd → substituí todas as ocorrências de /bin/bash do usuário root por /bin/false
$ sed -i 's/antigo/novo/g' arquivo.txt → substitui ocorrência da palavra "antigo" por "novo" em cada linha do arquivo e salva diretamente no arquivo sem mostrar no terminal
$ sed '/antigo/d' arquivo.txt → remove todas as linhas do arquivo que possuem a palavra “antigo”
$ sed '2,5d’ arquivo.txt → remove as linhas entre a 2ª e a 5ª linhas
$ sed '/root/,/daemon/d' /etc/passwd → remove todas as linhas que contém root e daemon
$ sed '/antigo/i Linha inserida antes' arquivo.txt → insere a frase antes de cada linha que tem a palavra “antigo”
$ sed -n '/antigo/p' arquivo.txt → exibe somente as linhas que contêm a palavra "sucesso" no arquivo
sed 's/antigo/novo/g' arquivo.txt > novo_arquivo.txt → substitui todas as ocorrências da palavra antigo pela palavra novo e direciona a saída para um novo arquivo
$ sed '3i john:x:1001:1001:John Doe,,,:/home/john:/bin/bash' /etc/passwd → insere uma linha (com a mensagem john:x:1001:1001:John Doe,,,:/home/john:/bin/bash) antes da terceira linha
$ sed '3a john:x:1002:1002:John Smith,,,:/home/john:/bin/bash' /etc/passwd  → insere uma linha depois da terceira linha
$ sed '$a jane:x:1003:1003:Jane Smith,,,:/home/jane:/bin/bash' /etc/passwd → insere uma linha depois da ultima linha
$ sed '/^daemon/i # Daemon line' /etc/passwd → adiciona uma linha antes de toda linha que comece com a palavra daemon
$ tail -f /var/log/syslog | sed '/daemon/i # Daemon line’ → mostra os arquivos atualizados em tempo real e adiciona uma linha antes de cada linha com a palavra Daemon

### Máterial Complementar:

---

## 4. `vi`

### Para que serve?

### Opções:

### Sintaxe comum:

### Exemplos:

### Máterial Complementar:

---

## 

### Para que serve?

### Opções:

### Sintaxe comum:

### Exemplos:

### Máterial Complementar:

---
