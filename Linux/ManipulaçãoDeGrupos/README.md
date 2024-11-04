# Comandos para Manipulação de Grupos

Nesta seção, exploramos comandos essenciais para manipulação de grupos no Linux. Esses comandos permitem **criar, modificar e excluir grupos, além de gerenciar a associação de usuários a esses grupos**.

Os seguintes comandos são utilizados de forma mais completa pelo usuário `root` ou super-usuários.

### Comandos:

1. [`groupadd`](#groupadd)
2. [`groupmod`](#groupmod)
3. [`groupdel`](#groupdel)
4. [`gpasswd`](#gpasswd)

## groupadd

### Para que serve?
O comando `groupadd` é utilizado para `criar novos grupos no sistema`. Este comando permite que administradores definam um **grupo no sistema com um _GID_ (valor numérico do ID do grupo) específico e outras opções de configuração**. Grupos no Linux são usados para gerenciar permissões de arquivos e diretórios para múltiplos usuários (que fazem parte de um mesmo grupo).

Quando um grupo é criado, ele é adicionado aos arquivos de sistema que gerenciam grupos, como `/etc/group`.

#### Arquivos relacionados:
- `/etc/group` → Contém informações sobre grupos de usuários no sistema.
- `/etc/login.defs` → Define parâmetros globais para criação de usuários e grupos, como os intervalos de GID e UID.

#### Configuração:
- **GID_MIN** `(1 000)` e **GID_MAX** `(60 000)` → Definem o intervalo de IDs de grupo que podem ser atribuídos a grupos regulares.
- **SYS_GID_MIN** `(101)` e **SYS_GID_MAX** `(999)` → Definem o intervalo de IDs de grupo para grupos de sistema.

### Opções:
- `-f` → Força a criação do grupo, esta opção faz com que o comando saia com status de sucesso se o grupo especificado já existir. Se `-f` é usado com `-g` , e o GID especificado já existe, outro GID (exclusivo) é escolhido.
- `-g` → Define o **GID**, deve estar entre o **GID_MIN** e o **GID_MAX**, e ser exclusivo, caso não seja o `groupadd` escolhe o menor **GID** disponível no intervalo configurado.
- `-K` → Substitui os valores padrão definidos em /etc/login.defs. Pode ser usado para definir valores como **GID_MIN** e **GID_MAX**.
- `-o` → Esta opção permite adicionar um grupo com um **GID** não exclusivo. Muito utilizado com `-g`.
- `-p` → Define uma senha criptografada para o grupo. Essa opção não é recomendada, pois pode ser vista em processos.
- `-r` → Cria um grupo de sistema, que terá um **GID** dentro do intervalo de grupos de sistema. Esses grupos são usados para funções específicas do sistema, e não para login de usuários regulares.
- `-R` → Aplica alterações no diretório **CHROOT_DIR** e usa os arquivos de configuração do diretório **CHROOT_DIR**.

### Sintaxe comum:
**`# groupadd [OPÇÕES] GRUPO`**

### Exemplos:
`# groupadd backend` → Cria o grupo `backend` com todos os dados no padrão.

`# groupadd -g 1010 backend` → Cria grupo `backend` com o **GID** `1010` exclusivo.

`# groupadd -f backend` → Cria o grupo `backend`, caso já exista mostra uma mensagem de sucesso.

`# groupadd -r backend_sistem` → Cria o grupo `backend_sistem` com um **GID** dentro do intervalo reservado para grupos de sistema.

`# groupadd -o -g 1000 backend2` → Cria o grupo `backend2` com um **GID** não exclusivo.

`# groupadd -K GID_MIN = 100` → Modifica o **GID** mínimo permitido no sistema.

`# groupadd -K GID_MAX = 499` → Modifica o **GID** máximo permitido no sistema.

### Máterial Complementar:
<img src="https://github.com/pedcravo/Wiki/blob/main/Linux/groupadd.png" width="600px">

https://www.linuxforce.com.br/comandos-linux/comandos-linux-comando-groupadd/

---

## groupmod

### Para que serve?

### Opções:

### Sintaxe comum:

### Exemplos:

### Máterial Complementar:

---

## groupdel

### Para que serve?

### Opções:

### Sintaxe comum:

### Exemplos:

### Máterial Complementar:

---

## gpasswd

### Para que serve?

### Opções:

### Sintaxe comum:

### Exemplos:

### Máterial Complementar:
