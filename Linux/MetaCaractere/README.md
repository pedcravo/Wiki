# Meta Caracteres no Linux

Os meta caracteres são símbolos especiais usados no terminal Linux para representar padrões em comandos e expressões regulares. Eles permitem realizar operações avançadas de busca, filtragem e manipulação de dados de forma eficiente.

### Comandos:

1. [`?`](#?)
2. [`.`](#.)
3. [`'`](#')
4. [`"`](#")
5. [`()`](#())
6. [`[]`](#[])
7. [`{}`](#{})
8. [`*`](#*)
9. [`\`](#\\)
10. [`^`](#^)
11. [`+`](#+)
12. [`$`](#$)

---

## `?`
Representa qualquer tipo de caractere (número, letra, caractere especial)

### Exemplos de uso:
**`ls` + `?` =**

`$ ls ???a` → Lista todos os itens do diretório atual que tenham 3 caracteres avulsos e que termine com “A”, como retorno pode ter: “maça”.

`$ ls ??a` → Lista todos os itens do diretório atual que tenham 2 caracteres avulsos e que termine com “A”, como retorno pode ter: “uva”.

`$ ls ???a` → Lista todos os itens do diretório atual que tenham 3 caracteres avulsos e que termine com “A”, como retorno pode ter: “maça”.

**`ls` + `?` + `*` =**

`$ ls ???*` → Lista todos os itens do diretório atual que tenham 3 caracteres avulsos e que termine com qualquer conjunto de caracteres, como retorno pode ter: “banana", “laranja",“maça", “maracuja",  “melancia”, “morango" e “uva".

`$ ls ??n*` → Lista todos os itens do diretório atual que tenham 2 caracteres avulsos, depois a letra “A” e que termine com qualquer conjunto de caracteres, como retorno pode ter: “banana”.

## `.`

## `'`

## `"`

## `()`

## `[]`

## `{}`

## `*`

## `\`

## `^`

## `+`

## `$`
