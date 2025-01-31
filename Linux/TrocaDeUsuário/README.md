# Comandos para troca de Usuário

Nesta sessão vamso ver sobre os comandos para trocar de usuário

---

## `su`
### Para que serve?
Utilizado para **mudar de usuário ou assumir a identidade de outro usuário no sistema.**

O comando `su` (substitute user) permite que você **troque para outro usuário** dentro da sessão atual do terminal. Quando usado sem especificar um nome de usuário, ele assume a identidade de root (superusuário).

Ao mudar de usuário, é solicitado que você forneça a senha do usuário que deseja acessar. Este comando é frequentemente usado para obter privilégios administrativos ou executar comandos como outro usuário sem fazer logout da sessão atual.

> **Sudoers** é um grupo de super usuários do Linux, por padrão o usuário root é o único como root 

### Opções:
- `-`, `-l`, `--login` → Permitem entrar no usuário desejado com uma interface semelhante ao iniciar sessão.
- `-c` → Permite executar um comando específico como outro usuário e, em seguida, retornar ao usuário original.
- `-s` → Especifica um shell alternativo para o novo usuário.
- `-p` → Preserva o ambiente do usuário atual ao mudar para outro usuário (variáveis, caminhos).
- `exit` → Sair do usuário (ou shell).

### Sintaxe comum:
**`$ su [OPÇÕES] USUARIO`**

### Exemplos:
`$ su` → Entra no usuário root permanecendo no local do usuário anterior.

`$ su -` → Entra no usuário root carregando o ambiente do *root*.

`$ su pedro1` → Conecta no usuário *pedro1* e pede senha para conectar-se nele, permanece no ambiente raiz do ultimo usuário conectado.

`$ su -l pedro1` → Conecta ao usuário e carrega sua área de trabalho semelhante ao inicio de sessão.

`$ su -c "ls -la" pedro1` → Entra no usuário *pedro1* somente para executar o comando, após isso retorna ao usuário que estava.

`$ su -s /bin/sh pedro1` → Entra no usuário *pedro1* iniciando no local */bin/sh*.

`$ su -p pedro1` → Entra no usuário pedro1 preservando as variáveis ambiente do usuário anterior.

### Máterial Complementar:
https://guialinux.uniriotec.br/su/

https://relaxaeusouti.com.br/2021/04/03/voce-sabe-a-diferenca-entre-os-comandos-su-e-su-no-gnu-linux/

---

## `sudo`
### Para que serve?
Utilizado para **executar comandos como superusuário (*root*)** ou como outro usuário, sem a necessidade de trocar de sessão.

O `sudo` (SUperuser DO) é uma ferramenta que permite a usuários autorizados executar comandos com privilégios elevados, fornecendo a senha do próprio usuário (em vez da senha do *root*).

> O `sudo` é frequentemente usado para realizar tarefas administrativas de maneira temporária, sem a necessidade de logar como *root* ou usar o comando `su` para mudar de usuário.

### Opções:
- `-i` → Abre um shell de login como *root*, carregando o ambiente de login completo (similar ao `su -`).
- `-k` → Invalida o cache de autenticação do *sudo*, forçando o próximo comando *sudo* a pedir a senha novamente (contrário do `-v`)
- `-l` → Lista os comandos que o usuário atual tem permissão para executar com `sudo`.
- `-s` → Inicia um shell interativo como *root* ou outro usuário.
- `-u` → Especifica o usuário como o qual o comando será executado (por padrão, o usuário é o *root*).
- `-v` → Revalida a autenticação sudo sem executar nenhum comando, pedindo a senha novamente para estender o período de autenticação (contrário do `-k`).

### Sintaxe comum:
**`$ sudo [OPÇÕES] COMANDO`**

### Exemplos:
`$ sudo apt update` → Executa o comando `apt` como *root*, após a execução retorna pro usuário anterior.

`$ sudo -u pedro mkdir diretorio` → Executa o comando `mkdir` como usuário *pedro*.

`$ sudo -l` → Exibe uma lista de comandos que o usuário atual pode executar com o *sudo*, de acordo com o arquivo */etc/sudoers*.