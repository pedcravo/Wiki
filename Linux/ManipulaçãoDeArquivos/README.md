
# Comandos para Manipulação de Arquivos
Nesta seção, exploramos comandos que permitem manipular arquivos e diretórios no Linux. Esses comandos são essenciais para **copiar, mover, alterar permissões, criar e remover arquivos e diretórios**.

### Comandos:

1. [`cp`](#cp)
2. [`dd`](#dd)
3. [`diff`](#diff) WIP
4. [`expand`](#expand)
5. [`unexpand`](#unexpand)
6. [`ln`](#ln)
7.  [`mv`](#mv)
8.  [`paste`](#paste)
9.  [`rm`](#rm)
10. [`mktemp`](#mktemp)
11. [`mkdir`](#mkdir)
12. [`rmdir`](#rmdir)
13. [`rsync`](#rsync)
14. [`split`](#split)
15. [`touch`](#touch)

---

## `cp`

### Para que serve?
Utilizado para **copiar arquivos ou diretórios** de um diretório para outro.

### Opções:
- `-i` → Faz checagem de segurança, se há um arquivo com este nome.
- `-l` → Cria links.
- `-n` → Não sobrescreve um arquivo existente.
- `-p` → Preserva os dados do arquivo original na cópia, como: data da modificação, tempo de acesso e permissão.
- `-r` → Pesquisa recursivamente nos diretórios.
- `-s` → Cria links simbólicos em vez de copiar arquivos (atualiza junto com o original).
- `-u` → Copia apenas quando o arquivo de origem é mais novo do que o arquivo de destino ou quando o arquivo de destino está faltando.
- `-v` → Mostra com mais detalhes o processo que está acontecendo.

### Sintaxe comum:
**`$ cp [OPÇÕES] ARQUIVO.. CÓPIA_ARQUIVO`**

### Exemplos:
$ cp exemploarquivo arquivoexemplo → copia o exemploarquivo trocando o nome para arquivoexemplo no mesmo diretório.

$ cp arquivo1.txt arquivo2.txt arquivo3.txt arquivo4.txt ~/Downloads/copias_arquivos → copia vários arquivos para dentro de um aquivo.

$ cp exemploarquivo /home/pedrocravo/Downloads/ → copia o exemploarquivo do local para o diretório Downloads.

$ cp /home/pedrocravo/Downloads/exemploarquivo arquivoexemplo → copia o arquivo do diretório Downloads para o local, dando a ele o nome arquivoexemplo.

$ cp ~/Documentos/[a-e]* ~/Downloads → copia arquivos ou diretórios do diretório Documentos que o nome começa com qualquer letra de "a" até "e", para o diretório Downloads.

$ cp ~/Documentos/[a]* exemplopasta → copia arquivos ou diretórios do diretório Documentos que o nome começa com "a", para o diretório exemplopasta (que está dentro do diretório Documentos).

$ cp -r diretorio1 diretorio2 → copia diretório com arquivos com recursão e da a cópia um novo nome.
$ cp -r diretorio /home/pedrocravo → copia diretório com arquivos para outro lugar.

### Máterial Complementar:
https://www.certificacaolinux.com.br/comando-linux-cp/

https://labex.io/tutorials/linux-linux-cp-command-file-copying-209744

---

## `diff`

### Para que serve?


### Opções:
- `opção` →

### Sintaxe comum:
**`Sintaxe`**

### Exemplos:
`Exemplo 1` →

`Exemplo 2` →

### Máterial Complementar:
https://link;comum.com.br/

---

## `dd`

### Para que serve?
O comando `dd` é utilizado no Linux para realizar a **cópia e conversão de dados entre arquivos ou dispositivos.** Ele é altamente flexível e pode ser usado para criar backups, clonar discos, gerar arquivos com tamanhos específicos, criar dispositivos bootáveis, entre outras tarefas relacionadas à manipulação de dados em baixo nível.

Funcionamento Geral:
• `if` (input file): Especifica o arquivo de origem.
• `of` (output file): Especifica o arquivo de destino.
• **Bloco de Leitura e Escrita:** A cópia é feita em blocos configuráveis, definidos por opções como `bs`, `ibs`, ou `obs`.
• **Conversões:** Permite converter formatos de dados, como transformar texto em maiúsculas, ou manipular bytes.

### Opções:
- `if=ARQUIVO` → Especifica o arquivo ou dispositivo de entrada (input file).
- `of=ARQUIVO` → Especifica o arquivo ou dispositivo de saída (output file).
- `bs=N` → Define o tamanho do bloco para leitura e escrita como N bytes (exemplo: bs=4M para blocos de 4 MB).
- `ibs=N` → Define o tamanho do bloco de entrada como N bytes.
- `obs=N` → Define o tamanho do bloco de saída como N bytes.
- `count=N` → Copia apenas N blocos da entrada.
- `skip=N` → Ignora os primeiros N blocos da entrada.
- `seek=N` → Pula os primeiros N blocos no arquivo de saída.
- `conv=tipo` → Realiza conversões específicas:
     1. `notrunc`: Não trunca o arquivo de saída.
     2. `sync`: Preenche blocos parciais com zeros.
     3. `ucase`: Converte para maiúsculas.
     4. `lcase`: Converte para minúsculas.
- `status=tipo` → Controla a saída do progresso:
     1. `none`: Suprime toda saída.
     2. `progress`: Mostra progresso durante a operação.

### Sintaxe comum:
**`$ dd if=ARQUIVO_ORIGEM of=ARQUIVO_DESTINO [OPÇÕES]`**

### Exemplos:
`$ dd if=/dev/cdrom of=imagem.iso bs=4M status=progress` → Copia os dados do dispositivo `/dev/cdrom` e cria um arquivo de imagem ISO chamado `imagem.iso` em blocos de 4 MB e exibe o progresso.

`# dd if=/dev/sda of=/dev/sdb bs=1M status=progress` → Clona o disco `/dev/sda` para `/dev/sdb` em blocos de 1 MB.

`$ dd if=/dev/zero of=arquivo_teste bs=1M count=100` → Cria um arquivo chamado `arquivo_teste` com 100 MB preenchidos com zeros.

`# dd if=arquivo.iso of=/dev/sdX bs=4M status=progress` → Escreve a imagem arquivo.iso diretamente no dispositivo `/dev/sdX` (substitua pelo seu dispositivo USB).

`# dd if=/dev/sda of=mbr_backup.img bs=512 count=1` → Copia os primeiros 512 bytes do disco `/dev/sda` (o MBR) para o arquivo `mbr_backup.img`.

`# dd if=mbr_backup.img of=/dev/sda bs=512 count=1` → Restaura o MBR salvo anteriormente no disco `/dev/sda`.

`$ echo "exemplo de texto" | dd conv=ucase` → Converte o texto de entrada para maiúsculas.

### Máterial Complementar:
https://www.linuxdescomplicado.com.br/2016/11/alguns-exemplos-de-que-o-comando-dd-pode-ser-considerado-umas-das-ferramentas-mais-versateis-do-linux.html

https://www.certificacaolinux.com.br/backup-do-mbr-com-o-comando-dd/

---

## `expand`

### Para que serve?
O comando `expand` é utilizado para **converter tabs em espaços** em um arquivo e quando nenhum arquivo é especificado, ele lê a partir da entrada padrão.

É interessante seu uso em scripts, para programadores é um comando excelente.

### Opções:
- `-i` → Converte apenas tabs iniciais, deixando tabs após espaços intactos.
- `-t N` → Define o número N de espaços que cada tabulação representará, com o padrão sendo 8.
- `-t LIST` → Define uma lista de posições de tabulação específicas separadas por vírgulas.

### Sintaxe comum:
**`$ expand [OPÇÕES] ARQUIVO`**

### Exemplos:
`$ expand arquivo.txt` → Converte todas as tabs para 8 espaços.

`$ expand --tabs=10 arquivo.txt > arquivo2.txt` → Converte cada tabs em 10 espaços e grava em arquivo2.txt.

`$ expand -t 4 -i documento.txt` → Converte apenas os tabs iniciais do arquivo para 4 espaços.

### Máterial Complementar:
https://www.linuxforce.com.br/comandos-linux/comandos-linux-comando-expand/

https://www.certificacaolinux.com.br/comando-linux-expand/

---

## `unexpand`

### Para que serve?
O comando `unexpand` é utilizado para **converter espaços em tabs em arquivos** de texto ou entrada padrão.

Esse comando é especialmente útil para reduzir o tamanho de arquivos que possuem grandes quantidades de espaços.

### Opções:
- `-a` → Converte todos os grupos de espaços em tabs, não apenas aqueles no início da linha.
- `--first-only` → Converte apenas os grupos iniciais de espaços em cada linha, padrão.
- `-t N` → Define a quantidade de espaços que um tab representa. O padrão é 8 espaços.
- `-t LIST` → Usa uma lista de posições separadas por vírgula para definir onde as tabulações devem ser colocadas.

### Sintaxe comum:
**`$ unexpand [OPÇÕES] ARQUIVO`**

### Exemplos:
`$ unexpand arquivo.txt` → Converte os espaços iniciais de cada linha em tabs.

`$ unexpand -a arquivo.txt` → Converte todos os espaços em tabs no arquivo inteiro.

`$ unexpand -t 4 arquivo.txt > arquivo_tabs.txt` → Converte grupos de 4 espaços em tabulações e grava no `arquivo_tabs.txt`.

`$ unexpand --tabs=4,8,12 arquivo.txt` → Usa posições de tabulação específicas para conversão, nos pontos definidos pela lista (4, 8 e 12).

### Máterial Complementar:
https://www.linuxforce.com.br/comandos-linux/comandos-linux-comando-expand/

https://www.certificacaolinux.com.br/comando-linux-expand/

---

## `ln`

### Para que serve?
O comando `ln` (Link) é utilizado para **criar links para arquivos ou diretórios no sistema Unix**, similar ao conceito de “atalho” em outros sistemas operacionais.

#### Tipos de Link
-  **Link Direto (Hard Link)** → Adiciona um novo nome para o mesmo arquivo (compartilha o mesmo inode). O arquivo só é removido do sistema quando o último link para ele é deletado. É uma referência direta ao conteúdo do arquivo.

- **Link Simbólico (Soft Link ou Symlink)** → Aponta para o caminho de um arquivo ou diretório (possui um inode próprio). É possível criar links simbólicos para arquivos em diferentes sistemas de arquivos ou diretórios, e o link permanece mesmo que o arquivo de destino seja excluído.

### Opções:
- `-d` → Cria um link direto, é o padrão.
- `-L` → Cria uma link para um link simbólico.
- `-s` → Cria uma link simbólico.
- `-t DIR` → Especifica o diretório `DIR` destino.
- `-v` → Mostra o nome de cada arquivo antes de criar o link.

### Sintaxe comum:
`$ ln [OPÇÕES] ORIGEM DESTINO`

### Exemplos:
`$ ln arquivo.txt linkdireto.txt` → Cria um link direto para `arquivo.txt` com o nome `linkdireto.txt`.

`$ ln -s /diretorio/exemplo linkexemplo` → Cria um link simbólico chamado `linkexemplo` para o diretório `/diretorio/exemplo`.

`$ ln -t /destino arquivo1 arquivo2` → Cria links diretos para `arquivo1` e `arquivo2` no diretório `/destino`.

`$ ln -s -v pasta_original/ pasta_link/` → Cria um link simbólico para `pasta_original` com o nome `pasta_link` e exibe o progresso.

### Máterial Complementar:
https://guialinux.uniriotec.br/ln/

---

## `mv`

### Para que serve?
O comando `mv` é utilizado para **mover ou renomear arquivos e diretórios**. Pode ser movido mais de um arquivo ou diretório ao mesmo tempo

Ficar atento a arquivos de mesmo nome, um arquivo sobrepõe outro sem perguntar.

### Opções:
- `-f` → Força a substituição dos arquivos existentes sem avisar.
- `-i` → Realiza checagem de segurança.
- `-n` → Não permite a sobrepoisção de arquivos.
- `-v` → Mostra na tela as ações executadas.

### Sintaxe comum:
**`$ mv [OPÇÕES] ARQUIVO.. DESTINO`**

### Exemplos:
`$ mv arquivo.txt ~/Downloads` → Move um arquivo para o diretório `Downloads`, a partir de qualquer diretório.

`$ mv arquivo1.txt arquivo2.txt Downloads/` → Move dois arquivos para o diretório `Downloads` a partir do `/home`.

`$ mv *.txt /Downloads/` → Move todos os arquivos `.txt` para o diretório `Downloads`.

`$ mv *.txt Downloads` → Move todos os arquivos com `.txt` para o diretório `Downloads`.

`$ mv arquivo.txt renomeado_arquivo.txt` → Renomeia o arquivo, utilizar o mesmo final `.txt`.

`$ mv Dir/ DirRenomeada/` → Renomeia um diretório no mesmo local em que estava o original.

`$ mv -i arquivo.txt Downloads` → Checa se tem arquivos com mesmo nome no local de destino.

`$ mv -n arquivo.txt Downloads` → Move um ou mais arquivos sem permitir a sobreposição no local de destino, neste caso `Downloads`.

`$ mv -v arquivo diretorio` → Move um arquivo mostrando na tela o caminho do que foi feita.

### Máterial Complementar:
https://labex.io/tutorials/linux-linux-mv-command-file-moving-and-renaming-209743

https://www.linuxforce.com.br/comandos-linux/comandos-linux-comando-mv/

---

## `paste`

### Para que serve?
O comando `paste` é utilizado para **unir dois arquivos tanto na tela quanto em um novo arquivo novo**.

### Opções:
- `-d` → Define um separador.
- `-s` → Troca a organização dos arquivos para uma coluna única.

### Sintaxe comum:
**`$ paste [OPÇÕES] ARQUIVO…`**

### Exemplos:
`$ paste arquivo1.txt arquivo2.txt` → Une linhas de arquivos lado a lado separador por tab.

`$ paste -d "," arquivo1.txt arquivo2.txt` → Une dois arquivos na tela e os separa com `,`.

`$ paste -s arquivo1.txt arquivo2.txt` → Une dois arquivos em somente uma coluna, um arquivo sobre o outro.

`$ paste arquivo1.txt arquivo2.txt > combinacao.txt` → Une dois arquivos em um aquivo novo.

### Máterial Complementar:
Não possui material complementar.

---

## `rm`

### Para que serve?
O comando `rm` é utilizado para **remover arquivos e diretórios cheios**. Pode ser removido mais de um arquivo ou diretório ao mesmo tempo.

### Opções:
- `-f` → Força a remoção.
- `-i` → Faz checagem de segurança.
- `-r` → Faz a remoção de diretório.

### Sintaxe comum:
**`$ rm [OPÇÕES] ITEM`**

### Exemplos:
`$ rm exemploarquivo.txt` → Remove arquivo.

`$ rm -r exemplopasta` → Remove diretório exemplopasta recursivamente, remove ele e tudo que tem dentro (diretórios e arquivos).

`$ rm -i arquivo.txt` → Questiona se realmente é para apagar a pasta.

`$ rm -f arquivo.txt` → Força a remoção do arquivo.

`$ rm -r exemplopasta` → Remove um diretório.

`$ rm -rf exemplopasta` → Força a remoção do diretório `exemplopasta` recursivamente.

### Máterial Complementar:
https://labex.io/tutorials/linux-linux-rm-command-file-removing-209741

---

## `mktemp`

### Para que serve?
O comando `mktemp` é usado para **criar arquivos e diretórios temporários de forma segura no Linux.** Esses arquivos ou diretórios recebem nomes únicos e geralmente são usados para armazenar dados temporários durante a execução de scripts ou comandos.

Os arquivos ou diretórios criados com `mktemp` não são automaticamente excluídos, a menos que sejam removidos explicitamente ou que o sistema seja reinicializado (dependendo da localização do arquivo).

### Opções:
- `-d` → Cria um diretório temporário em vez de um arquivo.
- `-p DIR` → Especifica o diretório onde o arquivo ou diretório temporário será criado.
- `-q` → Não exibe mensagens de erro no caso de falhas.
- `-t` → Usa um prefixo padrão e cria o arquivo ou diretório temporário no `/tmp`.
- `--suffix=SUFFIX` → Adiciona um sufixo ao nome do arquivo temporário.
- `-u` → Remove o arquivo ou diretório logo após a criação (geralmente não recomendado por motivos de segurança).

### Sintaxe comum:
**`$ mktemp [OPÇÕES] [PADRÃO]`**

### Exemplos:
`$ mktemp` → Cria um arquivo temporário com um nome único no diretório atual.

`$ mktemp -d` → Cria um diretório temporário no /tmp com um nome único.

`$ mktemp arquivo_XXXXXX` → Cria um arquivo com o prefixo "`arquivo_`" e substitui os "`X`" por caracteres aleatórios.

`$ mktemp -p /home/user/temp_files` → Cria o arquivo temporário no diretório /home/user/temp_files.

`$ mktemp --suffix=.log` → Cria um arquivo temporário que termina com a extensão `.log`.

`$ mktemp -u` → Cria um arquivo temporário e o remove em seguida.

### Máterial Complementar:
https://sempreupdate.com.br/linux/comandos/guia-completo-para-o-comando-mktemp-no-linux/

https://www.gnu.org/software/autogen/mktemp.html

---

## `mkdir`

### Para que serve?
O comando mkdir é utilizado para criar um ou mais diretórios.

### Opções:
- `-p` → Permite criar diretórios pais e filhos.
- `-v` → Mostra na tela as ações sendo executadas.

### Sintaxe comum:
**`$ mkdir [OPÇÕES] NOME_DIRETÓRIO`**

### Exemplos:
`$ mkdir exemplopasta` → Cria um diretório no local atual.

`$ mkdir dir1 dir2` → Cria 2 diretórios no local atual.

`$ mkdir /home/pedrocravo/Documentos/exemplopasta` → cria diretório no local `/home/pedrocravo/Documentos`.

`$ mkdir -p dirpai/dirmeio/dirfilho` → Cria diretórios em cadeia.

`$ mkdir -pv dirpai/dirmeio/dirfilho` → Cria diretórios em cadeia e mostra na tela o que está sendo feito.

### Máterial Complementar:
Não possui material complementar.

---

## `rmdir`

### Para que serve?
O comando `rmdir` é utilizado para **remover um ou mais diretórios vazios**.

### Opções:
- `-p` → Remove uma hierarquia de diretórios (recursivamente).
- `-v` → Exibe informações para cada diretório processado.

### Sintaxe comum:
**`$ rmdir [OPÇÕES] DIRETÓRIO...`**

### Exemplos:
`$ rmdir exemplopasta` → Remove diretório no local.

`$ rmdir dir1 dir2` → Remove dois diretórios no local.

`$ rmdir /home/pedrocravo/Documentos/exemplopasta` → Remove diretório no local `/home/pedrocravo/Documentos`.

`$ rmdir --ignore-fail-on-non-empty exemplopasta` → Remove diretório no local ignorando arquivos dentro dele.

### Máterial Complementar:
https://guialinux.uniriotec.br/rmdir/

---

## `rsync`

### Para que serve?
O comando `rsync` é uma ferramenta robusta para **copiar e sincronizar arquivos e diretórios de forma eficiente.** Ele utiliza um algoritmo que transfere apenas as diferenças entre a origem e o destino, economizando tempo e largura de banda.

- **Sincronizar arquivos e diretórios:** Pode ser usado localmente ou entre sistemas remotos via SSH.
- **Backup:** Ideal para backups incrementais, pois transfere apenas arquivos novos ou modificados.
- **Transferência eficiente:** Transfere dados usando compressão e verificações de integridade.

#### Arquivos Relacionados:
**Log de transferência:** É possível salvar logs de execução adicionando `--log-file=NOME_ARQUIVO`.

### Opções:
- `-a` → Habilita o modo de arquivamento, preserva permissões, timestamps, links simbólicos e mais.
- `-v` → Mostra os arquivos sendo transferidos.
- `-z` → Habilita compressão durante a transferência.
- `-r` → Copia diretórios recursivamente.
- `-u` → Evita substituir arquivos mais novos no destino.
- `-e` → Permite especificar um shell remoto, como SSH.
- `--progress` → Mostra o progresso detalhado da transferência.
- `-P` → Combina `--progress` e `--partial`, permitindo reiniciar transferências interrompidas.
- `--delete` → Remove do destino os arquivos que não estão na origem.
- `--exclude=PADRÃO` → Exclui arquivos ou diretórios que correspondem ao `PADRÃO` fornecido.
- `--dry-run` → Simula a execução do comando sem fazer alterações.
- `--bwlimit=KB/s` → Limita a largura de banda usada para a transferência.

### Sintaxe comum:
**`$ rsync [OPÇÕES] ORIGEM DESTINO`**

### Exemplos:
`$ rsync -av /origem/diretorio/ /destino/diretorio/` → Copia recursivamente todos os arquivos de `/origem/diretorio/` para `/destino/diretorio/`, preserva permissões, timestamps e links simbólicos. O uso de `/` ao final de `/origem/diretorio/` copia apenas o conteúdo, e não o diretório em si.

`$ rsync -avz -e ssh /origem/diretorio/ usuario@servidor:/destino/diretorio/` → Utiliza o SSH para transferir arquivos com segurança e comprime os dados durante a transferência.

`$ rsync -av --progress /origem/diretorio/ /destino/diretorio/` → Mostra os detalhes e progresso de cada arquivo sendo transferido.

`$ rsync -av --exclude="*.log" /origem/ /destino/` → Ignora arquivos com a extensão .log.

`$ rsync -av --delete /origem/ /destino/` → Remove do destino os arquivos que não existem mais na origem.

`$ rsync -av --dry-run /origem/ /destino/` → Mostra o que seria feito, sem realmente executar a sincronização.

`$ rsync -av --bwlimit=100 /origem/ usuario@servidor:/destino/` → Limita a transferência a `100 KB/s`.

---

## `split`

### Para que serve?
O comando `split` é utilizado para **dividir arquivos grandes em arquivos menores**, com base no número de linhas ou no tamanho em bytes. Esse comando é útil para processar ou transferir arquivos grandes em partes menores.

- O padrão é dividir o arquivo a cada **1000 linhas**.
- Os nomes dos arquivos de saída seguem o padrão arquivo**aa**, arquivos**ab**, arquivo**ac**, assim por diante. É possível especificar um sufixo para o arquivo de saída.

### Opções:
- `-a N` → Define o comprimento dos sufixos em `N` caracteres.
- `-b N` → Divide o arquivo em um número `N` de bytes.
- `-d` → Usa números como sufixos no lugar de letras.
- `-l N` ou `-N` → Onde `N` é o número de linhas que irão dividir o arquivo de entrada.

### Sintaxe comum:
**`$ split [OPÇÕES] ARQUIVO PREFIXO`**

### Exemplos:
`$ split -2 arquivo.txt lista_` → Divide o arquivo a cada 2 linhas, cada arquivo menor vai ter 2 linhas.

`$ split -a 3 -l 2 arquivo.txt parte_` → Divide arquivo em arquivos de 2 linhas cada, usando sufixos de 3 caracteres.

`$ split -b 1M arquivo.txt parte_` → Divide o arquivo em arquivos de 1 megabyte cada.

`$ split -b 1K arquivo.txt parte_` → Divide arquivo em arquivos de 1 KB cada.

`$ split -d -l 3 arquivo.txt parte_` → Divide arquivo em arquivos de 3 linhas cada, usando sufixos numéricos.

`$ split -d -a 3 -l 100 arquivo.txt parte_` → Divide arquivo em arquivos de 100 linhas cada, usando sufixos numéricos de 3 dígitos.

### Máterial Complementar:
https://www.certificacaolinux.com.br/comando-linux-split/

---

## `touch`

### Para que serve?
O comando `touch` é utilizado para **criar arquivos em branco ou atualizar a data e hora de modificação e acesso de arquivos existentes**. É uma maneira rápida de criar arquivos vazios ou ajustar os timestamps de arquivos.

É possível criar **mais de um arquivo ao mesmo tempo**, e caso o arquivo já exista, o `touch` não modifica seu conteúdo, apenas altera suas informações de data e hora.

### Opções:
- `-a` → Atualiza apenas o horário de acesso do arquivo, sem modificar o horário de modificação
- `-c` → Não cria o arquivo caso ele não exista. Apenas modifica a data e hora de arquivos que já existem.
- `-m` → Atualiza apenas o horário de modificação do arquivo, sem alterar o horário de acesso.
- `-r` → Usa o timestamp de outro arquivo para definir a data e hora de modificação do arquivo.
- `-t` → Define uma data e hora específicas para o arquivo, no formato [[CC]YY]MMDDhhmm[.ss] (ano, mês, dia, hora, minuto e segundos opcionais).

### Sintaxe comum:
**`$ touch [OPÇÕES] ARQUIVO`**

### Exemplos:
`$ touch arquivo` → Cria um arquivo comum.

`$ touch arquivo.txt` → Cria um arquivo `.txt`.

`$ touch .arquivo` → Cria um arquivo oculto.

`$ touch arquivo1.txt arquivo2.txt` → Cria dois arquivos `.txt`.

`$ touch -a arquivo.txt` → Atualiza a data de acesso de `arquivo.txt` sem modificar seu conteúdo.

`$ touch -t 202401011200 arquivo.txt` → Define a data e hora de `arquivo.txt` para 1º de janeiro de 2024, 12:00.

`$ touch -r modelo.txt novoarquivo.txt` → Copia a data e hora do arquivo `modelo.txt` para o arquivo `novoarquivo.txt`.

### Máterial Complementar:
Não possui material complementar.