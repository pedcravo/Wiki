# Comandos para Manipular usuários

Nesta sessão vamos ver os comandos que são utilizados para manipular usuários.

### Comandos:
1. [`useradd`](#useradd)
2. [`usermod`](#usermod)
3. [`userdel`](#userdel)
4. [`passwd`](#passwd)
5. [`pwquality`](#pwquality)

---

## `useradd`

### Para que serve?
Utilizado para **criar novos usuários ou definir configurações padrão para novos usuários no sistema**. O comando `useradd` é uma ferramenta de baixo nível no Linux para adicionar usuários, atualizando os arquivos do sistema e, opcionalmente, criando diretórios iniciais para os novos usuários.

Embora o `useradd` seja útil para operações diretas, é recomendado usar o comando `adduser` (uma interface mais amigável) em algumas distribuições, como o Ubuntu, que é derivada do Debian.

> **OBS:**
> A criação de novos usuários com o `useradd` pode depender de parâmetros e configurações definidas em arquivos do sistema, como `/etc/default/useradd` e `/etc/login.defs`.

A principal diferença entre o **diretório inicial de um usuário** e o **diretório shell** é que o primeiro é onde estão armazenadas as definições específicas do usuário, enquanto o segundo é o programa inicial que é executado após o login.

### Opções:
- `-c` → Define um comentário ou nome completo do usuário.
- `-d` → Define o diretório inicial do usuário.
- `-e` → Especifica a data de expiração da conta (no formato AAAA-MM-DD).
- `-g` → Define o grupo primário do novo usuário.
- `-G` → Adiciona o usuário a grupos adicionais.
- `-m` → Cria o diretório inicial do usuário. Caso o diretório não exista, ele será criado.
- `-s` → Define o shell de login do usuário.
- `-r` → Cria um usuário do sistema (para contas especiais que não têm login).
- `-D` → Sozinho mostra os valores padrão do sistema. Com qualquer opção **define novos valores padrão**, edita as variáveis padrões em  `/etc/default/useradd`.

#### Opções com o -D:
- `-b` → Define o caminho base para o diretório inicial do usuário, `/home/` **(define a variável `HOME`).** 
- `-e` → Define a data de expiração padrão **(define a variável `EXPIRE`).**
- `-f` → Define a quantidade de dias padrão após o vencimento de uma senha antes que a conta seja desativada **(define a variável `INATIVA`)**.
- `-g` → Define o nome ou id do grupo inicial padrão **(define a variável `GROUP`)**.
- `-s` → Define o shell padrão de logon de um novo usuário **(define a variável `SHELL`).**

### Sintaxe comum:
**`# useradd [OPÇÕES] USUARIO`**

### Exemplos:
`# useradd -c "Pedro Cravo" pedro` → Cria o usuário pedro e define o nome completo do usuário pedro.

`# useradd -d /home/dir_pedro pedro` → Define o diretório inicial do usuário pedro.

`# useradd -e 2024-12-31 pedro` → Cria o usuário com uma data de expiração da conta (dia 31/12/2024).

`# useradd -g backend pedro` → Cria o usuário pedro e define o grupo primário que irá participar.

`# useradd -G sudo,developers pedro` → Cria o usuário pedro e adiciona ele aos grupos sudo e developers.

`# useradd -m pedro` → Cria o usuário pedro juntamente com o diretório inicial dele `/home/pedro`.

`# useradd -s /bin/bash pedro` → Define qual shell vai ser direcionado o usuário ao fazer o login.

`# useradd -D` → Mostra o padrão do sistema para a criação de usuário.

`# useradd -D -e 2040-12-31` → Altera a data padrão de expiração de usuários para 31/12/2040.

### Máterial Complementar:
https://www.linuxforce.com.br/comandos-linux/comandos-linux-comando-useradd/

https://guialinux.uniriotec.br/useradd/

https://linuxconfig.org/how-to-create-modify-and-delete-users-account-on-linux

https://www.freecodecamp.org/news/how-to-manage-users-in-linux/

---

## `usermod`

### Para que serve?
Utilizado para modificar as configurações de uma conta de usuário existente

Geralmente utilizado por administradores. O comando `usermod` permite que administradores alterem várias propriedades de uma conta de usuário, como o **diretório inicial, grupos, shell de login, e data de expiração da conta.**

> **OBS:**
> Você deve garantir que o usuário nomeado não esteja executando nenhum processo quando este comando estiver sendo executado se o ID numérico do usuário, o nome do usuário ou o diretório inicial do usuário estiver sendo alterado.

#### Arquivos relacionados:
• `/etc/passwd`: Armazena informações sobre as contas de usuário.
• `/etc/shadowv`: Contém senhas e informações de expiração de contas.
• `/etc/group`: Informações sobre grupos.
• `/etc/gshadow`: Contém informações seguras sobre grupos.

### Opções:
- `-a` → Adiciona o usuário grupos suplementares (pode ser um ou mais) sem remove-lo dos grupos existentes. Só pode ser usado com `-G`.
- `-c` → Modifica o valor do campo de comentário do arquivo de senha do usuário, normalmente usado para adicionar o nome completo do usuário.
- `-d` → Altera o diretório de login de usuário, geralmente junto com `-m`.
- `-e` → Modifica a data em que a conta do usuário será desativada **(no formato AAAA-MM-DD)**.
- `-f` → Modifica o número de dias após o vencimento de uma senha em que a conta será desativada permanentemente (um valor 0 desativa a conta imediatamente após a senha expirar).
- `-g` → Modifica o grupo principal na qual o usuário faz parte, inserir nome ou número do grupo existente.
- `-G` → Modifica os grupos suplementares que o usuário faz parte, retira aqueles que ele já tem **(cada grupo é separado do próximo por uma vírgula, sem espaços em branco)**.
- `-l` → Modifica o nome do login do usuário, apenas.
- `-L` → Bloqueie a senha de um usuário. Isso coloca um ” ! ” Na frente da senha criptografada.
- `-m` → Move o diretório inicial do usuário para o novo local especificado com a opção `-d`.
- `-o` → Quando usada com a opção `-u`, essa opção permite alterar o ID do usuário para um valor não exclusivo.
- `-p` → Modifica a senha (criptografada ou não) do usuário
- `-s` → Altera o shell de login do usuário
- `-u` → Modifica o valor do ID do usuário
- `-U` → Desbloqueie a senha de um usuário permitindo fazer login novamente. Isso remove o ” ! ” na frente da senha criptografada.

> **OBS:**
> Os comandos `-L`, `-p` e `-U` não podem ser utilizados juntos, pois manipulam a senha do usuário.

### Sintaxe comum:
**`# usermod [OPÇÕES] LOGIN`**

### Exemplos:
`# usermod -a -G backend2 pedro` → Adiciona grupos já existentes ao usuário preservando aqueles que já pertence.

`# usermod -aG backend3 pedro` → Adiciona grupos já existentes ao usuário preservando aqueles que já pertence.

`# usermod -d /novo/dir_base -m pedro` → Altera o diretório inicial do usuário para /novo/dir_base.

`# usermod -e 2024-12-31 pedro` → Altera a data de expiração do usuário para 31/12/2024.

`# usermod -l pedro1 pedro` → Modifica o nome do usuário.

`# usermod -L pedro` → Bloqueia a senha do usuário, não possibilitando o login com a senha.

`# usermod -U pedro` → Desbloqueia o usuário.

### Máterial Complementar:
https://www.linuxforce.com.br/comandos-linux/comandos-linux-comando-usermod/

https://guialinux.uniriotec.br/usermod/

https://www.ibm.com/docs/pt-br/aix/7.3?topic=u-usermod-command

https://linuxconfig.org/how-to-create-modify-and-delete-users-account-on-linux

https://www.freecodecamp.org/news/how-to-manage-users-in-linux/

---

## `userdel`

### Para que serve?
Utilizado para **remover usuários do sistema** Linux. O comando `userdel` é uma ferramenta de baixo nível que exclui todas as entradas relacionadas ao usuário especificado em arquivos de sistema como `/etc/passwd` e `/etc/group`. É comumente utilizado por administradores de sistemas para deletar contas de usuários.

> **OBS:**
> Se a variável `USERGROUPS_ENAB` estiver definida como **yes** em `/etc/login.defs`, o `userdel` também removerá o grupo do usuário, caso ele não seja usado como grupo principal por outro usuário.

#### Arquivos relacionados:
• `/etc/passwd`: Armazena informações sobre contas de usuário.
• `/etc/group`: Armazena informações sobre grupos.
• `/etc/shadow`: Contém senhas e outras informações seguras de contas de usuário.

### Opções:
- `-f` → Força a remoção da conta do usuário, mesmo que o usuário ainda esteja logado. Também remove o diretório pessoal e o spool de correio, mesmo que outro usuário use o mesmo diretório pessoal ou se o spool não for de propriedade.
- `-r` → Remove o diretório inicial e o spool de correio do usuário, além de deletar a conta.
- `-R CHROOT_DIR` → Aplica a remoção de um usuário dentro de um ambiente chroot especificado.
- `-Z` → Remove qualquer mapeamento de usuário do SELinux (Security-Enhanced Linux) associado ao usuário.

### Sintaxe comum:
**`# userdel [OPÇÕES] LOGIN`**

### Exemplos:
`# userdel -f pedro` → Força a remoção do usuário ignorando se está conectado, seu diretório e seu correio.

`# userdel -r pedro` → Remove o usuário, seu diretório inicial (`/home/pedro/`) e o correio do usuário.

### Máterial Complementar:
https://www.linuxforce.com.br/comandos-linux/comandos-linux-comando-userdel/

https://linuxconfig.org/how-to-create-modify-and-delete-users-account-on-linux

https://www.freecodecamp.org/news/how-to-manage-users-in-linux/

---

## passwd

### Para que serve?
O comando `passwd` **configura e altera senhas de usuários**. Nesse comando qualquer usuário pode trocar sua senha, porém apenas o admin pode trocar a senha de outros usuários.

### Opções:
- `-d` → Exclui a senha de uma conta de usuário.
- `-e` → Força a conta de usuário a alterar a senha.
- `-l` → Bloqueia a conta de usuário.
- `-u` → Desbloqueia a conta de usuário.
- `-S` → Exibe informações sobre o status da senha de uma conta específica.
- `-w N` → O usuário receberá um alerta para mudar a senha `N` dias antes do limite da opção `-x`.
- `x`  → Define o número máximo de dias em que uma senha permaneça válida.

### Sintaxe comum:
**`$ passwd USUÁRIO`**

### Máterial Complementar:
https://www.ibm.com/docs/pt-br/power8?topic=commands-passwd-command

https://www.google.com/search?q=comando+passwd+linux&client=firefox-b-d&sca_esv=7d5f0fdd92d02893&sxsrf=ADLYWIIN_tN9B7-gbj3OiIEbF5eTPscTKQ%3A1729797260206&ei=jJwaZ6CUDJmh1sQPksW-0AQ&ved=0ahUKEwigiun53KeJAxWZkJUCHZKiD0oQ4dUDCBA&uact=5&oq=comando+passwd+linux&gs_lp=Egxnd3Mtd2l6LXNlcnAiFGNvbWFuZG8gcGFzc3dkIGxpbnV4MgUQABiABDIGEAAYFhgeMgYQABgWGB4yCBAAGBYYHhgPMggQABgWGB4YDzIKEAAYFhgKGB4YDzIIEAAYFhgeGA8yCBAAGIAEGKIEMggQABiABBiiBEjSJVCMHVioJHABeAGQAQCYAYIBoAHtBaoBAzAuNrgBA8gBAPgBAZgCB6AC2AbCAgoQABiwAxjWBBhHwgIIEAAYFhgKGB6YAwCIBgGQBgiSBwMxLjagB50k&sclient=gws-wiz-serp

---

## passwd

### Para que serve?
O `pwquality` é uma **ferramenta usada para definir e gerenciar políticas de senhas no sistema**, garantindo que as senhas dos usuários atendam a determinados critérios de segurança. Ele é configurado através do arquivo `/etc/security/pwquality.conf` e geralmente é integrado ao PAM (Pluggable Authentication Module) para aplicar as políticas durante a criação ou alteração de senhas.

O arquivo do programa está localizado no local: `/etc/security/pwquality.conf`, independente do SO. Este arquivo contém as diretrizes e opções configuráveis para as políticas de senha.

### Opções:
- `minlen=N` → Define o comprimento mínimo da senha (padrão: 8).
- `dcredit=N` → Define o número mínimo de dígitos exigidos na senha (valores negativos tornam opcional).
- `ucredit=N` → Define o número mínimo de letras maiúsculas exigidas na senha.
- `lcredit=N` → Define o número mínimo de letras minúsculas exigidas na senha.
- `ocredit=N` → Define o número mínimo de caracteres especiais exigidos na senha.
- `maxrepeat=N` → Limita o número máximo de repetições consecutivas de caracteres na senha.
- `maxclassrepeat=N` → Limita o número máximo de repetições de classes de caracteres.
- `maxsequence=N` → Limita o tamanho de sequências consecutivas na senha (ex: "12345").
- `gecoscheck=1` → Verifica se a senha não contém o nome do usuário ou informações do campo GECOS.
- `retry=N` → Número de tentativas permitidas para criar uma senha válida.

### Exemplos de configuração:
1. **Configurar políticas de senha com maior segurança:**
    ```bash
    minlen=12
    dcredit=-1
    ucredit=-1
    lcredit=-1
    ocredit=-1
    maxrepeat=2
    gecoscheck=1
    ```
    
    - Senhas devem ter no mínimo 12 caracteres.
    - É obrigatório incluir pelo menos 1 dígito, 1 letra maiúscula, 1 letra minúscula e 1 caractere especial.
    - Não são permitidas mais de 2 repetições consecutivas de caracteres.
  
2. **Editar arquivo PAM para usar pwquality:**
    Adicione ou edite a linha no arquivo `/etc/pam.d/common-password` (ou equivalente):
    
    ```bash
    password requisite pam_pwquality.so retry=3
    ```
    
    Limita as tentativas de criar uma senha válida para 3.
    
3. **Testar configuração:**
    Alterar a senha de um usuário para testar as políticas:
    ```bash
    $ passwd username
    ```

### Exemplos:
`# sudo apt install libpam-pwquality` → Instalar `pwquality`.

`# nano /etc/security/pwquality.conf` → Usado para editar o local do arquivo do programa.

`# sudo nano /etc/pam.d/common-password` → Aplicar alterações no PAM.

### Máterial Complementar:
https://linux.die.net/man/5/pwquality.conf