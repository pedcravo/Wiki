# Dicionário de Comandos Linux

Bem-vindo ao **Dicionário de Comandos Linux**! Este repositório contém uma coleção organizada de comandos Linux, divididos por temas com base em seus possíveis usos.  
Alguns comandos podem aparecer em mais de um tema e estão atualizados em todos os contextos.

Cada tema possui um README separado, contendo uma lista de comandos, suas descrições, opções, exemplos de uso e materiais complementares para aprofundar seu conhecimento.

---

## Informações adicionais

### Opções
No Linux, é importante saber que as opções, na maioria dos casos, podem ser combinadas. Por exemplo:  
```bash
$ tar -cvf compactado.tar ~/Downloads/arquivo
```
Aqui as opções `-c`, `-v` e `-f` são combinadas.

### Sintaxe comum
A maioria dos comandos segue uma **estrutura básica** de sintaxe, que define como eles devem ser digitados no terminal.

---

## Temas

### 1. [Ajuda](./Ajuda)  
Comandos para **obter informações e documentação sobre outros comandos** no terminal.  
Exemplos: `help`, `type`, `man`, `apropos`.

### 2. [Atalhos do teclado (terminal)](./AtalhosTeclado)  
Principais **atalhos de teclado** para melhorar a produtividade no terminal.  
Exemplos: `Ctrl+a`, `Ctrl+e`, `Tab`, `Ctrl+u`, `Ctrl+c`, `Ctrl+d`, `Ctrl+z`, `Ctrl+k`, `Ctrl+l`, `Ctrl+Alt+t`.

### 3. [Compactar e Combinar Arquivos](./Compactar|Combinar)  
Comandos para **combinar e compactar arquivos**, úteis para manipular grandes volumes de dados e economizar espaço.  
Exemplos: `cat`, `gzip`, `gunzip`, `join`, `paste`, `tar`, `zip`, `unzip`.

### 4. [Editores de Texto](./EditoresDeTexto)  
Ferramentas para **editar textos e manipular conteúdo** diretamente no terminal.  
Exemplos: `bash`, `nano`, `sed`, `vi`.

### 5. [Filtrar e Organizar Dados](./Filtrar|Organizar)  
Comandos para **filtrar, processar e organizar dados** no Linux.  
Exemplos: `cat`, `tac`, `cut`, `grep`, `awk`, `echo`, `head`, `tail`, `less`, `nl`, `sort`, `tr`, `uniq`, `wc`.

### 6. [Manipulação de Aplicações](./ManipulaçãoDeAplicações)  
Comandos para **gerenciar instalação e pacotes de software** no sistema.  
Exemplos: `apt`, `aptitude`, `configure`, `dpkg`, `flatpak`, `ppa`, `snap`.

### 7. [Manipulação de Arquivos](./ManipulaçãoDeArquivos)  
Comandos para **copiar, mover, criar, remover e sincronizar arquivos e diretórios**.  
Exemplos: `cp`, `dd`, `diff`, `expand`, `unexpand`, `ln`, `mv`, `paste`, `rm`, `mktemp`, `mkdir`, `rmdir`, `rsync`, `split`, `touch`.

### 8. [Manipulação de Grupos](./ManipulaçãoDeGrupos)  
Comandos para **criar, modificar e excluir grupos** e gerenciar membros.  
Exemplos: `groupadd`, `groupmod`, `groupdel`, `gpasswd`.

### 9. [Manipulação de Redes](./ManipulaçãoDeRedes)  
Ferramentas para **configuração e diagnóstico de redes** no Linux.  
Exemplos: `ab`, `arpwatch` e `iptraf`, `dnstop`, `hostname`, `ifconfig`, `ip`, `iperf`, `mii-tool` e `ethtool`, `mtr`, `netstat` e `ss`, `nmcli` e `nmtui`, `ping`, `fping` e `hping`, `ssh`, `sftp`.

### 10. [Manipulação de Usuários](./ManipulaçãoDeUsuários)  
Comandos para **criar, modificar e excluir usuários** e gerenciar senhas.  
Exemplos: `useradd`, `usermod`, `userdel`, `passwd`, `pwquality`.

### 11. [Manipulação de Variáveis](./ManipulaçãoDeVariaveis)  
Explicações sobre **variáveis e aliases** no Linux e como manipulá-los.  
Exemplos: variáveis (`$HOME`, `$USER`, `$SHELL`, `$PWD`, `$PATH`, `$TERM`, `$LANG`), comandos (`env`, `printenv`, `set`, `export`, `unset`, `declare`), e criação de aliases (`alias`).

### 12. [Manipulação do Sistema](./ManipulaçãoDoSistema)  
Comandos para **monitoramento, agendamento e configuração do sistema**.  
Exemplos: `&`, `at`, `bg`, `fg`, `cron` e `anacron`, `date`, `fdisk`, `free`, `history`, `iostat`, `vmstat`, `jobs`, `kill`, `modprobe`, `mount` e `unmount`, `nice`, `ionice`, `renice`, `pgrep`, `ps`, `pstree`, `swapon`, `systemctl`, `tmux`, `top`, `htop`, `tty`, `tzselect`, `uname`, `uptime`.

### 13. [Metacaracteres e Expressões Regulares](./MetaCaractere)  
Símbolos especiais usados em comandos e buscas para **criar padrões e filtros avançados**.  
Exemplos: `?`, `.`, `'`, `"`, `()`, `[]`, `{}`, `*`, `\`, `^`, `+`, `$`.

### 14. [Navegação Pelo Sistema](./NavegaçãoPeloSistema)  
Comandos para **mover-se entre diretórios e visualizar a estrutura de arquivos**.  
Exemplos: `cd`, `dir`, `ls`, `pwd`, `tree`.

### 15. [Operadores Lógicos](./OperadoresLógicos)  
Operadores para **encadear comandos** no bash.  
Exemplos: `;`, `&&`, `||`.

### 16. [Gerenciadores de Permissões](./Permissões)  
Comandos para **visualizar e alterar permissões de arquivos e diretórios**.  
Exemplos: `chmod`, `chown`, `chgrp`.

### 17. [Pesquisa Pelo Sistema](./PesquisaPeloSistema)  
Comandos para **procurar arquivos, processos, dispositivos e informações** no sistema.  
Exemplos: `apropos`, `dmesg`, `find`, `inxi`, `journalctl`, `locate`, `ls`, `lscpu`, `lsmod`, `lsof`, `lspci`, `lsusb`, `netstat` e `ss`, `pvdisplay`, `sar`, `ss`.

### 18. [Redirecionamento: Stdin, Stdout e Stderr](./Stdin|Stdout|Stderr)  
Formas de **redirecionar entrada, saída e erros** no terminal.  
Exemplos: `<`, `>`, `>>`, `|`, `tee`, `2>`, `2>>`, `xargs`.

### 19. [Troca de Usuário](./TrocaDeUsuário)  
Comandos para **alternar entre usuários** ou executar ações como outro usuário.  
Exemplos: `su`, `sudo`.