# Comandos para Manipulação de Grupos

Nesta seção, exploramos comandos essenciais para manipulação de grupos no Linux. Esses comandos permitem **criar, modificar e excluir grupos, além de gerenciar a associação de usuários a esses grupos**.

### Comandos:

1. [`groupadd`](#1-groupadd)
2. [`groupmod`](#2-groupmod)
3. [`groupdel`](#3-groupdel)
4. [`gpasswd`](#4-gpasswd)

## 1. groupadd

### Para que serve?
O comando `groupadd` é utilizado para `criar novos grupos no sistema`. Este comando permite que administradores definam um **grupo no sistema com um _ID de grupo_ (GID) específico e outras opções de configuração**. Grupos no Linux são usados para gerenciar permissões de arquivos e diretórios para múltiplos usuários (que fazem parte de um mesmo grupo).

Quando um grupo é criado, ele é adicionado aos arquivos de sistema que gerenciam grupos, como `/etc/group`.

#### Arquivos relacionados:
• `/etc/group` → Contém informações sobre grupos de usuários no sistema.
• `/etc/login.defs` → Define parâmetros globais para criação de usuários e grupos, como os intervalos de GID e UID.

#### Configuração:
• `GID_MIN (1 000)` e `GID_MAX (60 000)` → Definem o intervalo de IDs de grupo que podem ser atribuídos a grupos regulares.
• `SYS_GID_MIN (101)` e `SYS_GID_MAX (999)` → Definem o intervalo de IDs de grupo para grupos de sistema.

### Opções:

### Sintaxe comum:

### Exemplos:

### Máterial Complementar:

---

## 2. groupmod

### Para que serve?

### Opções:

### Sintaxe comum:

### Exemplos:

### Máterial Complementar:

---

## 3. groupdel

### Para que serve?

### Opções:

### Sintaxe comum:

### Exemplos:

### Máterial Complementar:

---

## 4. gpasswd

### Para que serve?

### Opções:

### Sintaxe comum:

### Exemplos:

### Máterial Complementar:
