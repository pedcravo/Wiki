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
Representa qualquer tipo de caractere (número, letra, caractere especial).

### Exemplos:
**`ls` + `?` =**

`$ ls ???a` → Lista todos os itens do diretório atual que tenham 3 caracteres avulsos e que termine com _A_, como retorno pode ter: _“maça”_.

`$ ls ??a` → Lista todos os itens do diretório atual que tenham 2 caracteres avulsos e que termine com _A_, como retorno pode ter: _“uva”_.

`$ ls ???a` → Lista todos os itens do diretório atual que tenham 3 caracteres avulsos e que termine com _A_, como retorno pode ter: _“maça”_.

**`ls` + `?` + `*` =**

`$ ls ???*` → Lista todos os itens do diretório atual que tenham 3 caracteres avulsos e que termine com qualquer conjunto de caracteres, como retorno pode ter: _“banana"_, _“laranja"_, _“maça"_, _“maracuja"_,  _“melancia”_, _“morango"_ e _“uva"_.

`$ ls ??n*` → Lista todos os itens do diretório atual que tenham 2 caracteres avulsos, depois a letra _A_ e que termine com qualquer conjunto de caracteres, como retorno pode ter: _“banana”_.

---

## `.`
Utilizado para indicar qualquer caractere menos uma linha em branco. 

---

## `'`
Utilizadas para delimitar o texto dentro delas como caracteres literais não interpretando nenhum como meta caractere.
Forma mais geral do `\`.

---

## `"`
Utilizadas para delimitar o texto dentro delas como caracteres literais exceto os sinais `$` e `\`. 

---

## `()`
Agrupa expressões para tratá-las como uma única unidade.
---

## `[]`
Representa qualquer um dos caractéres que estão entre colchetes
Pode incluir letras, número separados por `-`.

### Formas de uso:
- `[aeiou]` → Uma sequência de caracteres dentro de colchetes é interpretada como todos os caracteres são válidos para a busca, ou seja, qualquer um dos caracteres dentro dos colchetes será correspondido.
- `[a-z]` → O sinal menos indica que qualquer caractere entre as letras _a_ e _z_ são válidos.
- `[0-9]` → Indica que qualquer número entre _0_ e _9_ é válido para a busca.
- `[^abc]` → Indica que qualquer caractere menos as letras _a_, _b_ e _c_ são válidos na busca, qualquer caractere que não esteja dentro dos colchetes será correspondido.

### Exemplos:
**`ls` + `[] `=**

`$ ls [a-n]aracuja` → Lista todos os itens do diretório atual que comecem com algma das letras entre _A_ e _N_ , como retorno pode ter: _“maracuja”_.

**`ls` + `[]` + `* `=**

$ ls [a-l]* → lista todos os itens do diretório atual que comecem com algma das letras entre _A_ e _L_ e que termine com qualquer conjunto de caracteres, como retorno pode ter: _“banana"_ e _“laranja"_.

---

## `{}`
Utilizado para expandir um conjunto de caracteres.

### Formas de uso
- `-` → Combina duas listas (é possivel fazer utilizando somente `{}` sem espaços).
- `{n}` → Caractere precedente deve aparecer exatamente `n` vezes.
- `{min,max}` → O caractere precedente deve aparecer pelo menos `min` vezes e no máximo `max` vezes.

### Exemplos:
**`touch` + `{}` =**

`$ touch arquivo{1,2,3,4,5}` → Cria 5 arquivos com nomes: _arquivo1_, _arquivo2_, _arquivo3_, _arquivo4_ e _arquivo5_.

`$ touch {Joao,Ana,Maria}-{Café,Almoço,Janta}` → cria arquivos combinados da primeira com a segunda lista, semelhante a recursão da arvore binária.

`$ touch {a ..f}{1.5}` → Cria arquivos combinados da primeira com a segunda lista.

---

## `*`
Representa qualquer caractere e número deste (0 ou mais caracteres), ou qualquer quantidade do caractere anterior a ele (grep).
**Não importam quantos e nem quais caracteres.**

### Exemplos:
**`ls` + `*` =**

`$ ls m*` → Lista todos os itens do diretório atual que tenham o nome com _M_ e qualquer conjunto de caracteres depois, como retorno pode ter: _“maracuja”_, _“melancia”_ e _“morango"_.

`$ ls m*a` → Lista os itens do diretório que tenham o nome com _M_, qualquer conjunto de caracteres depois e _A_ no final, como retorno pode ter: _“maracuja”_ e _“melancia”_.

`$ ls *n*` → Lista os itens do diretório que tenham o nome com qualquer conjunto de caracteres, depois _n_ e qualquer conjunto de caracteres no final, como retorno pode ter: _“banana"_, _“laranja"_, _“morango"_ e _“melancia”_.

`$ ls u*a*` → Lista os itens do diretório que tenham o nome com _U_, qualquer conjunto de caracteres, depois _A_ e qualquer conjunto de caracteres no final, como retorno pode ter: _“uva"_.

**`ls` + `?` + `*` =**

`$ ls ???*` → Lista todos os itens do diretório atual que tenham 3 caracteres avulsos e que termine com qualquer conjunto de caracteres, como retorno pode ter: _“banana"_, _“laranja"_, _“maça"_, _“maracuja"_,  _“melancia”_, _“morango"_ e _“uva"_.

`$ ls ??n*` → Lista todos os itens do diretório atual que tenham 2 caracteres avulsos, depois a letra _A_ e que termine com qualquer conjunto de caracteres, como retorno pode ter: _“banana”_.

**`grep` + `*` =**

`$ cat grep-file.txt | grep 'ss*'` → Mostra todas as linhas que tenham um ou dois _s_, pode ter como retorno: _"expressão"_ e _"sapo"_.

`$ cat grep-file.txt | grep 'ess*'` → Mostra todas as linhas que tenham _es_ ou _ess_, pode ter como retorno: _"expressão"_ e _"teste"_.

---

## `\`
Usado para mostrar que caracteres especiais ou meta caracteres devem ser interpretados como caracteres comuns.
Pode ser usado em qualquer meta caractere.

### Forma de uso:
- `\^` → Interpreta `^` como um caractere comum.
- `\/` → Não considera `/` como um diretório.
- `Área\ de\ Trabalho/` → Interpreta os espaços como caracteres pertencentes ao nome do diretório.

---

## `^`
Geralmente utilizado para indicar inicio de linha ou linha iniciada por determinado caractere.

### Forma de uso:
- `^a` → Se refere a letra a como primeiro caractere.
- `^[aeiou]` → Se refere a qualquer letra dentro do `[]` como primeiro caractere.
- `^.[aeiou]` → Se refere a qualquer letra dentro do `[]` como segundo caractere, tem um caractere antes.

---

## `+`
Representa um ou mais caracteres (1 ou mais).
**Não importam quantos e nem quais caracteres.**

---

## `$`
Geralmente utilizado para indicar final de linha ou determinado caractere utilizado no fim da linha (0 ou 1 vez).
