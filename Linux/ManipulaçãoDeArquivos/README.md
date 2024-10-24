# Comandos para Manipulação de Arquivos

Nesta seção, exploramos comandos que permitem manipular arquivos e diretórios no Linux. Esses comandos são essenciais para copiar, mover, alterar permissões, criar e remover arquivos e diretórios.

### Comandos:

1. [`chgrp`](#1-chgrp)
2. [`chmod`](#2-chmod)
3. [`chown`](#3-chown)
4. [`cp`](#4-cp)
5. [`ln`](#5-ln)
6. [`mkdir`](#6-mkdir)
7. [`mv`](#7-mv)
8. [`paste`](#8-paste)
9. [`rm`](#9-rm)
10. [`rmdir`](#10-rmdir)
11. [`touch`](#11-touch)

---

## 1. `chgrp`

### Para que serve?
O comando `chgrp` (Change Group) é usado para **modificar a propriedade do grupo associado a um arquivo**, permitindo que grupos diferentes tenham controle de leitura, escrita ou execução sobre o arquivo.

Esse comando é especialmente útil em ambientes multi usuário, onde diferentes grupos de trabalho precisam gerenciar arquivos em conjunto.

#### Arquivos Relacionados:
- `/etc/group`: Contém informações sobre grupos de usuários no sistema.

### Opções:
- `-c` → Exibe as alterações feitas. Similar ao `-v`, mas mostra apenas quando uma alteração de grupo ocorre.
- `-f` → Suprime a maioria das mensagens de erro. Se houver falhas no comando, elas não serão exibidas no terminal.
- `-h` → Afeta links simbólicos em vez dos arquivos apontados por eles. Usado em sistemas que permitem alterar a propriedade de links simbólicos.
- `-R` → Aplica a mudança de grupo a todos os arquivos e subdiretórios dentro de um diretório.
- `--reference=RFILE` → Altera o grupo de um arquivo ou diretório com base nas permissões de grupo do `RFILE` especificado.
- `-v` → Mostra um diagnóstico para cada arquivo processado, independentemente de ter sido alterado ou não.

### Sintaxe comum:
**`$ chgrp [OPÇÕES] GRUPO ARQUIVO`**

### Exemplos:
`# chgrp backend file.txt` → Altera o grupo proprietário do arquivo para o grupo `backend`.

`# chgrp -R staff /office/files` → Altera recursivamente o grupo de todos os arquivos e diretórios dentro de `/office/files`.

`# chgrp --reference=arquivo.exe file.txt` → Altera o grupo do arquivo `file.txt` para o mesmo grupo de `arquivo.exe`.

`# chgrp -h backend link_sim` → Altera o grupo dono do link simbólico sem alterar o arquivo base (o arquivo na qual ele aponta).

### Máterial Complementar:
https://www.linuxforce.com.br/comandos-linux/comandos-linux-comando-chgrp/

![Screenshot 2024-10-24 at 14-46-34 Captura_de_tela_de_2024-10-17_16-55-01 webp (imagem WEBP 662 × 294 pixels)](https://github.com/user-attachments/assets/9db3d0a3-1461-4c46-96c6-f90ba2019a61)

---

## 2. `chmod`

### Para que serve?

### Opções:

### Sintaxe comum:

### Exemplos:

### Máterial Complementar:

---

## 3. `chown`

### Para que serve?

### Opções:

### Sintaxe comum:

### Exemplos:

### Máterial Complementar:

---

## 4. `cp`

### Para que serve?

### Opções:

### Sintaxe comum:

### Exemplos:

### Máterial Complementar:

---

## 5. `ln`

### Para que serve?

### Opções:

### Sintaxe comum:

### Exemplos:

### Máterial Complementar:

---

## 6. `mkdir`

### Para que serve?

### Opções:

### Sintaxe comum:

### Exemplos:

### Máterial Complementar:

---

## 7. `mv`

### Para que serve?

### Opções:

### Sintaxe comum:

### Exemplos:

### Máterial Complementar:

---

## 8. `paste`

### Para que serve?

### Opções:

### Sintaxe comum:

### Exemplos:

### Máterial Complementar:

---

## 9. `rm`

### Para que serve?

### Opções:

### Sintaxe comum:

### Exemplos:

### Máterial Complementar:

---

## 10. `rmdir`

### Para que serve?

### Opções:

### Sintaxe comum:

### Exemplos:

### Máterial Complementar:

---

## 11. `touch`

### Para que serve?

### Opções:

### Sintaxe comum:

### Exemplos:

### Máterial Complementar:
