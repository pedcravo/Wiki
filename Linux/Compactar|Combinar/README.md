# Comandos de Compactar e Combinar Arquivos

Nesta seção, exploramos comandos que permitem combinar ou compactar arquivos no Linux. Esses comandos são úteis para manipular grandes quantidades de dados e reduzir o espaço de armazenamento ocupado por arquivos.

### Comandos:

1. [`cat`](#1-cat)
2. [`gzip`](#2-gzip)
3. [`gunzip`](#3-gunzip)
4. [`tar`](#4-tar)
5. [`zip`](#5-zip)
6. [`unzip`](#6-unzip)

---

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
O comando `gzip` é usado para **compactar arquivos**. Ele aplica algoritmos de compressão para reduzir o tamanho dos arquivos e adicionar a extensão `.gz` ao nome.
Pode ser utilizado no usuário comum, porém o **uso é mais limitado**.

**Aplica algoritmos para remover redundância em dados, tornando o arquivo menor.**

### Opções:
- `-c` → Grava o resultado na saída padrão e mantém o arquivo original inalterado.
- `-d` → Descompacta (semelhante ao comando `gunzip`).
- `-l` → Lista informações sobre os arquivos compactados/descompactados.
- `-r` → Compacta/descompacta recursivamente (navega a estrutura de diretórios recursivamente).
- `-t` → Verifica a integridade do arquivo compactado.

### Sintaxe comum:
`$ gzip [OPÇÕES] ARQUIVO`

### Exemplos:
`$ gzip arquivo` → Compacta `arquivo`.

`$ gzip -d arquivo.txt.gz` → Descompacta o arquivo com `.gz` (arquivo descompactado → `arquivo.txt`).

`$ gzip compactado.tar` → Compacta arquivo `.tar` (adiciona `.gz` a ele).

`$ gzip -c arquivo.txt `[`>`](./Stdin|Stdout|Stderr)` arquivo.gz` → Compacta o arquivo na saída padrão sem alterar o arquivo original (`arquivo.txt`), sobrescreve o resultado da saída padrão no `arquivo.gz`. Veja mais sobre o comando > em 

/Stdin|Stdout|Stderr/

`$ gzip -c arquivo.txt >> arquivo.gz`  → Compacta o arquivo na saída padrão sem alterar o arquivo original (arquivo.txt), concatena o resultado da saída padrão no arquivo.gz (caso não exista o arquivo destino, ele cria)

### Máterial Complementar:

---

## 3. `gunzip`

`# gunzip arquivo` → descompacta arquivo caso exista um com este nome e extensão .gz, caso não exista ele compacta o arquivo existente

`# gunzip arquivo` → descompacta arquivo com extensão .gz 

`# gunzip -c arquivo.txt.gz` > arquivo.txt → descompacta o arquivo na saída padrão sem alterar o arquivo original (arquivo.txt.gz), sobrescreve o resultado da saída padrão no arquivo.txt (caso não exista o arquivo destino, ele cria)

`# gunzip -c arquivo.txt.gz` > /home/pedrocravo/Downloads/arquivo.txt → faz o mesmo do comando anterior, manda o resultado para o arquivo no local indicado
