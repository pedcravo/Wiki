# Variáveis e Alías

Nesta sessão iremos ver um pouco de como funcionam as variaveis e alias no linux.

## Variáveis

As váriaveis são utilizadas para guardar palavras, local de diretórios, comandos, etc.

Exitem dois tipos de variáveis:
**Var Shell (Locais)** → Tipo de variável que só existe durante o tempo em que o Shell estiver aberto (é sempre temporária).
**Var de Ambiente (Global)** → Tipo de variável que pode ser editada e acessada de qualquer lugar do sistema (inclusive por arquivos), pode ser temporária ou permanentemente.

### Principais Variáveis Globais:
- `$HOME` → Aponta para a área de trabalho.
- `$USER` → Contém o nome do usuário.
- `$SHELL` → Contém o local comum do shell.
- `$PWD` → Contém o diretório atual.
- `$PATH` → Utilizado para armazenar uma lista de diretórios onde o sistema procura por de comandos.
- `$TERM` → Contém o nome especifico do terminal que emula o Shell.
- `$LANG` → Contém a linguagem do linux.

### Comandos para manipular Variáveis
- `env` → Visualiza todas as variáveis existentes no ambiente virtual (ENVironment).
- `printenv` → Também exibe as variáveis de ambiente, mas permite procurar variáveis específicas.
- `set` → Exibe todas as variáveis, incluindo variáveis locais e de shell.
- `export` → Usado para exportar uma variável local e torná-la uma variável de ambiente ou criar uma variável de ambiente.
- `unset` → Remove uma variável.
- `declare` → Usado para declarar variáveis e funções. Ele também pode ser usado para definir variáveis só de leitura.

### Criando variáveis
`$ my_local_var="Olá, sou uma variável local”` → Cria a variável local `$my_local_var`.

`$ export MY_ENV_VAR="Olá, sou uma variável Global”` → Cria a variável ambiente `$ MY_ENV_VAR`.

`$ declare -r VARIAVEL_IMUTAVEL="valor"` → Declara variável imutável.

### Mostra variáveis
`$ env | sort` → Organiza as variáveis ambiente em ordem alfabética.

`$ env | grep MY_ENV_VAR` → Procura pela variável criada.

`$ printenv USER` → Procura pela variável criada.

`$ echo $my_local_var` → Mostra o conteúdo da variável na tela.

`$ echo $MY_ENV_VAR` → Mostra na tela o conteúdo da variável.

`$ echo "$MY_ENV_VAR"` → Mostra na telam o conteúdo da variável.

`$ echo '$my_loccal_var'` → Mostra na tela o nome da variável.

`$ echo "O valor de my_var é: $my_var”` → Mostra uma frase + variável.

```bash
$ echo '#!/bin/bash
echo "Shell variable: $my_local_var"
echo "Environment variable: $MY_ENV_VAR"' > test_vars.sh
```
→ Cria um arquivo com os comandos acima, ao executar o arquivo a mensagem é:
```bash
Shell variable:
Environment variable: variavel global
```

### Tornando variável permanente
`$ nano ~/.bashrc` → Entra no arquivo bash para edita-lo e adicionar: `export MY_VAR_PERM="Este é um valor permanente"`.

`$ source ~/.bashrc` → Rodar o código.

`$ nano ~/.bashrc` → Entra no arquivo bash para edita-lo e retirar a linha do export: `export MY_VAR_PERM="Este é um valor permanente"`.

`$ source ~/.bashrc` → Rodar o código.

### Material de apoio
https://labex.io/tutorials/linux-environment-variables-in-linux-385274

https://diolinux.com.br/tutoriais/como-configurar-a-path-no-linux.html

https://www.linkedin.com/pulse/how-commands-work-linux-path-variable-explained-shafeeque-aslam/

## Alías

Utilizado para **substituir comandos longos ou complexos por comandos mais curtos ou fáceis de lembrar**. Ao definir um alias, você pode simplificar a execução de comandos frequentes, economizando tempo e esforço.

> **OBS:**
> Os aliases funcionam no sistema chave-valor.

### Sintaxe comum:
`$ alias NOME='comando'`

### Para criar alias:
`$ alias c=’cd /home/Downloads’` → Cria um alias com nome c para o comando cd /home/Downloads.

`$ alias rm=’rm -i’` → Criar um alias de rm para o comando `rm -i`.

`$ alias atualizar='sudo apt update && sudo apt upgrade'` → Cria um alisa de comandos encadeados.

### Para tornar um alias permanente:
`$ nano ~/.bashrc` → Entra no arquivo bash para editá-lo e adicionar: `$ alias c=’cd /home/Downloads’`.

`$ source ~/.bashrc` → Rodar o código.

`$ nano ~/.bashrc` → Entra no arquivo bash para editá-lo e retirar a linha do export: `$ alias c=’cd /home/Downloads’`.

`$ source ~/.bashrc` → Rodar o código.