# Comandos de Compactar e Combinar Arquivos

Nesta seção, exploramos comandos que permitem combinar ou compactar arquivos no Linux. Esses comandos são úteis para manipular grandes quantidades de dados e reduzir o espaço de armazenamento ocupado por arquivos.

### Comandos:

1. [`cat`](#1-cat)
2. [`gzip`](#2-gzip)
3. [`gunzip`](#3-gunzip)
4. [`join`](#4-join)
5. [`tar`](#5-tar)
6. [`zip`](#6-zip)
7. [`unzip`](#7-unzip)

## 1. `cat`

### Para que serve?
O comando `cat` é utilizado para **juntar (concatenar) arquivos**. Em sua forma base, ele também pode ser utilizado para **visualizar o conteúdo de arquivos** diretamente no terminal.

### Opções:
- `-n` → Mostra os números de cada linha do arquivo.
- `-v` → Mostra caracteres não imprimíveis, como acentos ou quebras de linha.

### Sintaxe comum:
`$ cat [OPÇÕES] ARQUIVO`

### Exemplos:
`$ cat arquivo.txt` → Mostra o arquivo `.txt` na tela.

`$ cat arquivo.txt - arquivo1.txt` → Mostra o arquivo .txt na tela e redireciona o conteúdo para outro arquivo `.txt`.

`$ cat arquivo1.txt arquivo2.txt > arquivo_combinado.txt` → Mostra os arquivos .txt na tela na tela e concatena ambos em um arquivo novo `.txt`.

`$ cat > arquivo_novo.txt` → Cria um novo arquivo e permite inserir dados manualmente (uma linha).

`$ cat >> arquivo.txt` → Atualiza o arquivo `.txt` ao invés de sobrescrevê-lo.

`$ cat -n arquivo1.txt` → Mostra a numeração de cada linha.

`$ cat -v arquivo2.txt` → Mostra caracteres não imprimíveis.

### Máterial Complementar:
https://ryanstutorials.net/linuxtutorial/vi.php

---

## 2. `gzip`

### Para que serve?
O comando `gzip` é usado para **compactar arquivos**. Aplica algoritmos de compressão para reduzir o tamanho dos arquivos e adicionar a extensão `.gz` ao nome.
Pode ser utilizado no usuário comum, porém o **uso é mais limitado**.

**Aplica algoritmos para remover redundância em dados, tornando o arquivo menor.**

### Opções:
- `-c` → Grava o resultado na saída padrão e mantém o arquivo original inalterado.
- `-d` → Descompacta (semelhante ao comando `gunzip`).
- `-l` → Lista informações sobre os arquivos compactados/descompactados.
- `-r` → Compacta/descompacta recursivamente (navega a estrutura de diretórios recursivamente).
- `-t` → Verifica a integridade do arquivo compactado.

### Sintaxe comum:
**`$ gzip [OPÇÕES] ARQUIVO`**

### Exemplos:
`$ gzip arquivo` → Compacta `arquivo`.

`$ gzip -d arquivo.txt.gz` → Descompacta o arquivo com `.gz` (arquivo descompactado → `arquivo.txt`).

`$ gzip compactado.tar` → Compacta arquivo `.tar` (adiciona `.gz` a ele).

`$ gzip -c arquivo.txt > arquivo.gz` → Compacta o arquivo na saída padrão sem alterar o arquivo original (`arquivo.txt`), sobrescreve o resultado da saída padrão no `arquivo.gz`.

`$ gzip -c arquivo.txt >> arquivo.gz`  → Compacta o arquivo na saída padrão sem alterar o arquivo original, concatena o resultado da saída padrão no `arquivo.gz`.

### Máterial Complementar:
https://guialinux.uniriotec.br/gzip/

https://labex.io/tutorials/linux-file-packaging-and-compression-385413

---

## 3. `gunzip`

### Para que serve?
Utilizado para **descompactar arquivos no formato `.gz`**. O comando `gunzip` é a ferramenta complementar ao `gzip`, permitindo a **reversão da compactação** aplicada por ele. Ele restaura o arquivo ao seu estado original antes da compressão.
Pode ser utilizado no usuário comum, porém o **uso é mais limitado**.

**Se um arquivo não existe no formato `.gz`, o comando tentará compactá-lo.**

### Opções:
- `-c` → Descompacta o arquivo para a saída padrão sem modificar o arquivo `.gz` original.
- `-f` → Força a descompactação, mesmo que o arquivo já exista. Substitui o arquivo existente sem solicitar confirmação.
- `-l` → Lista as informações sobre o arquivo compactado, incluindo o tamanho antes e depois da compressão e a taxa de compressão.
- `-r` → Descompacta recursivamente arquivos em diretórios. Descompacta todos os arquivos `.gz` encontrados em um diretório e seus subdiretórios.

### Sintaxe comum:
**`$ gunzip [OPÇÕES] ARQUIVO`**

### Exemplos:
`$ gunzip arquivo` → Descompacta arquivo caso exista um com este nome e extensão `.gz`, caso não exista ele compacta o arquivo existente.

`$ gunzip -c arquivo.txt.gz > arquivo.txt` → Descompacta o arquivo na saída padrão sem alterar o arquivo original, sobrescreve o resultado da saída padrão no `arquivo.txt`.

`$ gunzip -c arquivo.txt.gz > /home/pedrocravo/Downloads/arquivo.txt` → Faz o mesmo do comando anterior, manda o resultado para o arquivo no local indicado.

`$ gunzip -r /home/pedrocravo/pasta` → Descompacta todos os arquivos `.gz` dentro do diretório especificado e seus subdiretórios.

`$ gunzip -l arquivo.txt.gz` → Exibe o tamanho original, compactado e a taxa de compressão do arquivo.

### Máterial Complementar:
https://www.linuxforce.com.br/comandos-linux/comandos-linux-comando-gunzip/

---

## 4. `join`

### Para que serve?
O comando `join` **concatena registros de dois arquivos de texto baseado em índices comuns** entre os registros.

 O comando funciona como um tipo de banco de dados primitivo, permitindo a montagem de novos arquivos de registros a partir de registros existentes em diferentes arquivos.

### Opções:
- `-1 C` e `-2 C` → Define quais colunas (`C`) de cada arquivo serão utilizados para a junção.
- `-a A` → Permite saída de linhas que não condizem nos arquivos, selecionar número `A` do arquivo.
- `-e` → Define um valor específico para preencher campos vazios quando uma correspondência não é encontrada em um dos arquivos.
- `-i` → Faz a comparação entre os valores dos campos ignorando a diferença entre maiúsculas e minúsculas.
- `-t` → Especifica separador (padrão é `:`).
- `-o A.C,A.C` → Edita ordem da saída, onde `A` é arquivo e `C` é coluna.
- `-v A` → Exibe somente as linhas que não condizem com o outro arquivo, as linhas solitárias.

### Sintaxe comum:
**`$ join [OPÇÃO] ARQUIVO1 ARQUIVO2`**

### Exemplos:
`$ join employees.txt salaries.txt` → Mostra o conteúdo dos dois arquivos unidos usando como base o id de cada linha (1ª coluna).

`$ join -o 1.2,1.3,2.2,1.1 employees.txt salaries.txt` → Altera a ordem de saída dos dados, o primeiro a sair é o _1.2_ (arquivo 1, coluna 2), _1.3_ (arquivo 1, coluna 3), _2.2_ (arquivo 2, coluna 2) e _1.1_ (arquivo 1, coluna 1).

`$ join -a 1 employees.txt salaries.txt` → Mostra todas as linhas do primeiro arquivo, até mesmo aquelas que não condizem com o outro arquivo.

`$ join -1 3 -2 1 employees.txt departments.txt` → Mostra a união entre os dois arquivos só que usando como base outra coluna, coluna `3` do arquivo employees.txt e coluna `1` de `departments.txt`.

### Máterial Complementar:
https://labex.io/tutorials/linux-linux-join-command-file-joining-219193

https://www.vivaolinux.com.br/dica/O-comando-join

---

## 5. `tar`

### Para que serve?
Utilizado para **combinar e compactar múltiplos arquivos e diretórios** em um único arquivo com a extensão `.tar`.
O `tar` (**Tape ARchive**) é uma ferramenta essencial no Linux para criar **arquivos compactados que agrupam dados em um único pacote, sem alterar o conteúdo**.
Pode ser combinado com outros algoritmos de compressão para gerar arquivos `.tar.gz`, `.tar.bz2`, ou `.tgz`.

**O arquivo `.tar` em si não é compactado, ele apenas agrupa**; a compactação é feita em conjunto com `gzip`, `bzip2`, etc.
Diferença de tamanho:
- `.tar`: apenas o agrupamento com `tar`.
- `.tar.gz`/`.tgz`: compressão com `tar` + `gzip`.
- `.tar.bz2`: compressão mais eficiente com `tar` + `bzip2`.

Pode ser utilizado no usuário comum, porém o **uso é mais limitado**.

### Opções:
- `-c` → Cria um novo arquivo .tar.
- `-f` → Especifica o nome do arquivo final (com extensão `.tar`).
- `-r` → Adiciona arquivos a um arquivo `.tar` existente.
- `-t` → Lista os arquivos dentro do arquivo compactado sem descompactar.
- `-v` → Mostra o progresso da compactação (modo detalhado).
- `-x` → Extrai arquivos de um arquivo `.tar` (pode extrair todo o conteúdo ou arquivos específicos).
- `-C` → Define o diretório de destino para onde os arquivos serão extraídos.

#### Compactadores Adicionais:
- `-z` → Compacta o arquivo usando `gzip`, gerando `.tar.gz` ou `.tgz`.
- `-j` → Compacta usando `bzip2`, gerando `.tar.bz2`.

### Sintaxe comum:
**`$ tar [OPÇÕES] ARQ_FINAL DIR/ARQ_BASE`**

### Exemplos:
`$ tar -cvf compactado.tar ~/Downloads/arquivo` → Compacta o arquivo com caminho `~/Downloads/arquivo` transformando-o no arquivo `compactado.tar`

`$ tar -cvf compactado.tar /home/diretorio` → Compacta o diretório `/home/diretorio` em `compactado.tar` e mostra na tela o processo.

`$ tar -cvzf compactado.tar.gz /home/diretorio` → Cria um arquivo compactado do diretório usando `gzip` criando o arquivo `compactado.tar.gz`, mostra o processo na tela.

`$ tar -cvjf compactado.tar.bz2 /home/diretorio` → Compacta o diretório usando `bzip2`, criando `compactado.tar.bz2`.

`$ tar -rvf compactado.tar adicionar.txt` → Adiciona arquivo `.txt`  ao arquivo `compactado.tar`, mostra na tela o que está ocorrendo.

`$ tar -tvf compactado.tar` → Lista os arquivos presentes no arquivo compactado sem extrair.

`$ tar -xvf compactado.tar` → extrai os arquivos e visualiza o processo

`$ tar -xvf compactado.tar -C /home/pedrocravo/Downloads` → Extrai arquivos com um diretório destino.

`$ tar -xvf compactado.tar Downloads/diretorio/arquivo1.txt` → Extrai somente o arquivo `Downloads/diretorio/arquivo1.txt`.

`$ tar -zxvf compactado.tar.gz Downloads/diretorio/arquivo2.txt` → Extrai somente o arquivo `Downloads/diretorio/arquivo2.txt`.

`$ tar --extract --file=compactado.tar Downloads/diretorio/arquivo3.txt` → extrai somente o arquivo `Downloads/diretorio/arquivo1.txt`

`$ tar -xvf compactado.tar --wildcards '*.txt'` → Extrai apenas os arquivos `.txt` e visualiza o processo.

### Máterial Complementar:
https://labex.io/tutorials/linux-file-packaging-and-compression-385413

---

## 6. `zip`

### Para que serve?
Utilizado para **compactar arquivos e diretórios no formato `.zip`**, que é amplamente utilizado em plataformas como Linux, Windows e macOS. Ele agrupa múltiplos arquivos em um único arquivo compactado, tornando-o mais fácil de armazenar e principalmente compartilhar.

Pode ser utilizado no usuário comum, porém o **uso é mais limitado**.

### Opções:
- `-e` → Protege arquivo compactado com senha (pede senha ao descompactar).
- `-r` → Compacta recursivamente diretórios, seus subdiretórios e todos os arquivos contidos neles.

### Sintaxe comum:
**`$ zip [OPÇÕES] ARQ_FINAL ARQ_BASE`**

### Exemplos:
`$ zip arquivo.zip arquivo1.txt arquivo2.txt arquivo3.txt` → Compacta diversos arquivos ao mesmo tempo.

`$ zip arquivo.zip arquivo4.txt` → Adiciona um arquivo a compactação já existente.

`$ zip -r arquivo_recursivo.zip Downloads/` → Faz uma compactação recursiva pela pasta `Downloads/`.

`$ zip -e comp_c_senha.zip arquivo.txt` → Compacta um arquivo com senha.

### Máterial Complementar:
https://labex.io/tutorials/linux-file-packaging-and-compression-385413

https://www.vivaolinux.com.br/dica/Uso-basico-dos-comandos-zip-e-unzip

---

## 7. `unzip`

### Para que serve?
Utilizado para **descompactar arquivos `.zip`**. O comando `unzip` é a ferramenta padrão para extrair arquivos que foram compactados com o comando `zip`.

Por padrão, ele descompacta o conteúdo no diretório atual, mas você pode especificar um diretório de destino para extrair os arquivos.

Pode ser utilizado no usuário comum, porém o **uso é mais limitado**.

### Opções:
- `-d` → Especifica o diretório de destino para onde os arquivos descompactados serão extraídos.
- `-l` → Lista o conteúdo do arquivo `.zip` sem descompactá-lo.

### Sintaxe comum:
**`$ unzip [OPÇÕES] /DESTINO/ ARQUIVO_COMP`**

### Exemplos:
`$ unzip arquivo.zip` → Descompacta `arquivo.zip`

`$ unzip -d /Downloads/dir arquivo.zip` → Descompacta arquivo no local `/Downloads/dir`

`$ unzip -l arquivo.zip` → Lista o conteúdo do arquivo compactado.

### Máterial Complementar:
https://www.vivaolinux.com.br/dica/Uso-basico-dos-comandos-zip-e-unzip
