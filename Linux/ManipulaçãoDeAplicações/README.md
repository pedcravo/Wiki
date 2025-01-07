# Comandos para Manipular aplicações

Nesta sessão vamos ver os comandos que são utilizados para manipular aplicações.

### Comandos:
1. [`apt`](#apt)
2. [`aptitude`](#aptitude)
3. [`conigure`](#configure)
4. [`dpkg`](#dpkg)
5. [`flatpak`](#flatpak)
6. [`ppa`](#ppa)
7. [`snap`](#snap)


## `apt`

### Para que serve?
O comando `apt` é o gerenciador de pacotes padrão em distribuições Debian e Ubuntu. O comando `apt` facilita a **instalação, atualização, remoção e limpeza de pacotes, sendo essencial para manter o sistema operacional atualizado e seguro.**

O `apt` combina funcionalidades básicas do `apt-get` e `apt-cache`, facilitando o uso para operações de manutenção de pacotes.

Para ter informações completas é necessário utilizar o usuário `root`.

### Opções:
- `update` → Atualiza a lista de pacotes disponíveis nos repositórios configurados, mas não realiza nenhuma alteração nos pacotes instalados.
- `upgrade` → Atualiza todos os pacotes instalados para suas versões mais recentes disponíveis nos repositórios. Não remove pacotes ou instala novos.
- `full-upgrade` → Atualiza todos os pacotes instalados, mas pode instalar novos pacotes ou remover os que causam conflitos. Útil para atualizações mais profundas.
- `dist-upgrade` → Similar ao full-upgrade, realiza atualizações de pacotes que incluem mudanças no sistema, como novas dependências ou remoção de pacotes antigos.
- `install` → Instala um pacote. Pode ser usado para pacotes específicos.
- `remove` → Remove um pacote instalado, mas mantém arquivos de configuração.
- `purge` → Remove completamente o pacote, incluindo os arquivos de configuração.
- `autoremove` → Remove pacotes que foram instalados automaticamente para resolver dependências, mas que agora não são mais necessários. Remove pacotes dependentes juntamente com o pacote que está sendo desinstalado.
- `clean` → Remove todos os arquivos de pacotes baixados do cache local.
- `autoclean` → Remove apenas os arquivos de pacotes antigos e desatualizados do cache local.
- `-y` → Assuma a resposta “sim” a qualquer prompt, prosseguindo com todas as operações, se possível.

### Sintaxe comum:
**`$ apt [OPÇÕES] [PACOTE]`**

### Exemplos:
`# apt update` → Atualiza a lista de pacotes.

`# apt upgrade -y` → Atualiza todos os pacotes instalados para suas versões mais recentes, caso tenha algum prompt a resposta é sempre sim.

`# apt-get dist-upgrade -y` → Realiza atualizações de pacotes que incluem mudanças no sistema, caso tenha algum prompt a resposta é sempre sim.

`# apt full-upgrade` → Atualiza pacotes, permitindo remover pacotes conflitantes ou instalar novos.

`# apt autoclean` → Limpa pacotes desatualizados do cache local.

`# apt clean` → Limpa todos os arquivos baixados de pacotes no cache local.

`# apt remove wget` →  Remove o pacote `wget`.

`# apt purge wget` → Remove completamente o pacote `wget` e seus arquivos de configuração.

### Máterial Complementar:


---

## `aptitude`

### Para que serve?
O comando `aptitude` é uma **ferramenta de gerenciamento de pacotes no Debian e em distribuições** Linux baseadas nele, como o Ubuntu. Semelhante ao `apt` e `apt-get`, ele é usado para instalar, atualizar, remover e pesquisar pacotes.

`Aptitude` inclui uma interface interativa que torna o processo de navegação e configuração de pacotes mais intuitivo, mas também pode ser usado como um comando em linha de comando.

### Opções:
- `g` → Usada dentro da interface para acessar a tela de confirmação e para confirmar ações (install e uninstall).
- `+` → Adicionar itens para install.
- `-` → Adicionar itens para uninstall.

### Sintaxe comum:
**`# aptitude [OPÇÕES]`**

### Exemplos:
`# aptitude` → Abre interface de instalação.

---

## `configure`

### Para que serve?
O comando `configure` é utilizado em sistemas Linux/Unix para **preparar um pacote de software para compilação e instalação.** Ele é um script autogerado pela ferramenta *Autoconf* e verifica o ambiente do sistema para garantir que todas as dependências e configurações necessárias estejam disponíveis antes de compilar o software.
O `configure` ajusta automaticamente as configurações do sistema ao pacote, criando um arquivo `Makefile` personalizado para a execução do comando `make`.

**Funcionalidades principais:**
- **Detectar dependências:** Verifica se as bibliotecas e ferramentas necessárias estão disponíveis no sistema.
- **Configuração personalizada:** Permite ao usuário definir diretórios de instalação, habilitar ou desabilitar recursos do pacote.
- **Flexibilidade do sistema:** Garante que o pacote seja compatível com diferentes sistemas e ambientes.

### Opções:
- `--prefix=DIRETÓRIO` → Especifica o diretório onde o software será instalado. O padrão é /usr/local.
- `--disable-FEATURE` → Desabilita uma funcionalidade específica do pacote.
- `--enable-FEATURE` → Habilita uma funcionalidade específica do pacote.
- `--with-PACKAGE` → Força a inclusão de uma biblioteca ou recurso adicional.
- `--without-PACKAGE` → Exclui uma biblioteca ou recurso adicional.

### Sintaxe comum:
**`$ ./configure [OPÇÕES]`**

---

## `dpkg`

### Para que serve?
O comando `dpkg` (Debian Package) é o gerenciador de pacotes padrão dos sistemas baseados em Debian, como Ubuntu e Debian. Ele é utilizado para **instalar, remover, listar e manipular pacotes** `.deb`.

Diferente de gerenciadores como o `apt`, o `dpkg` é um gerenciador de pacotes de baixo nível, não lida com dependências automaticamente, sendo normalmente usado para instalações mais diretas ou para gerenciamento de pacotes já localizados no sistema.

Para ter informações completas é necessário utilizar o usuário `root`.

### Opções:
- `-c` ou `--contents` → Lista o conteúdo de um pacote `.deb`.
- `--configure` → Reconfigura os pacotes indicados que tenham sido parcialmente instalados, completando a instalação.
- `--force-[opções]` → Força a execução de operações, ignorando problemas específicos (por exemplo, `--force-conflicts`).
- `--get-selections` → Lista todos os pacotes instalados, com seu status (instalado, removido, etc.).
- `-i` ou `--install` → Instala um pacote .deb.
- `-l` ou `--list` → Lista o status de um pacote específico ou todos os pacotes, se nenhum pacote for especificado.
- `-L` ou `--listfiles` → Exibe todos os arquivos de um pacote instalado.
- `-P` ou `--purge` → Remove um pacote, seus arquivos de configuração e suas dependências.
- `-r` ou `--remove` → Remove um pacote, mantendo os arquivos de configuração.
- `-S` ou `--search` → Identifica o pacote que forneceu um arquivo específico.
- `-s` ou `--status` → Exibe o status detalhado de um pacote.
- `--verify` → Verifica se o pacote está com todos os dados íntegros.
- `--unpack` → Extrai os arquivos de um pacote .deb, sem configurar.

### Sintaxe comum:
**`# dpkg [opções] [pacote]`**

### Exemplos:
`# dpkg -r vim` → Remove o pacote `vim`, mas mantém os arquivos de configuração.

`# dpkg -P vim` → Remove o pacote `vim` e seus arquivos de configuração.

`# dpkg -L vim` → Lista todos os arquivos instalados pelo pacote.

`# dpkg -S /usr/bin/python3` → Identifica qual pacote contém o arquivo `/usr/bin/python3`.

`# dpkg -s vim` → Exibe informações detalhadas sobre o status do pacote `vim`.

`# dpkg --configure -a` → Configura todos os pacotes parcialmente instalados.

`# dpkg -s vim` → Este comando consulta o status detalhado do pacote `vim`.

`# dpkg -l vim` → Este comando lista todos os pacotes instalados e verifica se o `vim` está instalado.

`# dpkg -l | grep vim` → Este comando lista todos os pacotes instalados e, em seguida, usa `grep` para filtrar as linhas que contêm o termo "vim".

`# dpkg -l | less` → Mostra com less uma lista de todos os processos do sistema.

`# dpkg -i automake_1.15.1-3ubuntu2_all.deb` → Instala o programa com base em seu arquivo `.deb` baixado.


`# dpkg-reconfigure tzdata` → É utilizado para configurar a data e hora do sistema (abre uma aba e atualiza automaticamente).

`# dpkg-reconfigure locales` → É utilizado para configurar o idioma, ordenação, país e etc abre uma aba e atualiza automaticamente).

`# dpkg-reconfigure console-data` → Reconfigura o teclado, muda a identificação do mapa do teclado no sistema, é necessário ser instalado pelo comando:`# apt-get install console-data`.

`# dpkg-reconfigure console-setup` → Reconfigura a codificação do console, dentre elas: `ISO`, `UTF-8`. etc.

### Máterial Complementar:

https://github.com/pedcravo/Wiki/blob/main/Linux/Aula 3 - Instalação de programas de Baixo Nível - DPKG.txt

---

## `ppa`

### Para que serve?
O `PPA` (Personal Package Archive) é uma funcionalidade do sistema de gerenciamento de pacotes do Ubuntu e derivados que **permite aos usuários adicionar repositórios personalizados ao sistema.** Esses repositórios são mantidos por indivíduos ou organizações, permitindo o acesso a versões mais recentes ou alternativas de softwares que podem não estar disponíveis nos repositórios oficiais do sistema.

O comando principal usado para gerenciar PPAs é o `add-apt-repository`.

---

## `flatpak`

### Para que serve?
O comando `flatpak` é utilizado para **gerenciar aplicativos empacotados no formato Flatpak**. Ele permite instalar, atualizar, remover e listar aplicativos, bem como manipular repositórios. Flatpak é amplamente usado para executar aplicativos de maneira isolada (sandboxing), garantindo maior segurança e compatibilidade entre distribuições Linux.

### Opções:
- `-c` → Exibe a quantidade de cada linha duplicada.
- `install [repositório] [aplicativo]` → Instala um aplicativo do repositório especificado.
- `uninstall [aplicativo]` → Remove um aplicativo instalado.
- `update [aplicativo]` → Atualiza o aplicativo para a versão mais recente disponível.
- list → Lista os aplicativos Flatpak instalados no sistema.
- `search [nome]` → Pesquisa aplicativos disponíveis nos repositórios configurados.
- `info [aplicativo]` → Exibe informações detalhadas sobre um aplicativo instalado ou disponível.
- `remote-add [nome] [URL]` → Adiciona um repositório remoto para instalação de aplicativos.
- `remote-list` → Lista os repositórios configurados no sistema.
- `run [aplicativo]` → Executa um aplicativo instalado via Flatpak.
- `remove [aplicativo]` → Remove um aplicativo instalado, incluindo suas permissões e arquivos associados.

### Sintaxe comum:
**`$ flatpak [OPÇÕES] [COMANDO]`**

### Exemplos:
`$ flatpak install flathub org.mozilla.firefox` → Instala o navegador Firefox do repositório Flathub.

`$ flatpak update` → Atualiza todos os aplicativos instalados para a versão mais recente.

`$ flatpak list` → Exibe todos os aplicativos instalados via Flatpak.

`$ flatpak run org.mozilla.firefox` → Executa o aplicativo Firefox instalado via Flatpak.

`$ flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo` → Adiciona o repositório Flathub ao sistema.

`$ flatpak remove org.mozilla.firefox` → Remove o Firefox instalado via Flatpak.

### Máterial Complementar:
https://diolinux.com.br/flatpak/como-instalar-o-suporte-flatpak-nas-distros-linux.html

https://flatpak.org/setup/Ubuntu

https://docs.flatpak.org/pt-br/latest/using-flatpak.html

https://plus.diolinux.com.br/t/comandos-basicos-para-gerenciar-pacotes-flatpak-no-linux/35809

---

## `snap`

### Para que serve?
O `snap` serve para **instalar, atualizar, remover e gerenciar pacotes Snap**. Esses pacotes são projetados para fornecer aplicativos em contêineres que isolam o software do sistema operacional principal, garantindo que ele funcione corretamente e de maneira independente, mesmo em sistemas diferentes.

**Canais de atualização:** O Snap permite diferentes canais de atualização (como `stable`, `beta`, `edge`), com diferentes níveis de estabilidade.

**Segurança:** Snaps são executados em contêineres, o que adiciona uma camada de segurança e isolamento ao software.

### Opções:
- `connect` → Conecta uma interface de slot e plug de um Snap, permitindo a integração com dispositivos ou serviços do sistema.
- `disconnect` → Desconecta uma interface que foi previamente conectada a um slot ou plug.
- `find` → Pesquisa pacotes (pelo nome) no repositório Snap para encontrar aplicativos disponíveis.
- `install` → Instala um pacote Snap.
- `list` → Lista todos os Snaps instalados no sistema.
- `refresh` → Atualiza o pacote Snap para a versão mais recente. Se não for especificado um pacote, todos os Snaps são atualizados.
- `remove` → Remove um pacote Snap do sistema.
- `revert` → Reverte um Snap para a versão anterior, caso uma atualização tenha causado problemas.
- `services` →  Lista os serviços Snap em execução e seu status.
- `stop` → Para um serviço Snap específico.
- `switch` →Altera o canal de atualização do Snap, como stable, beta, edge, ou candidate.
- `version` → Exibe a versão do Snap instalada no sistema.

### Sintaxe comum:
**`$ snap [OPÇÕES] [PACOTE]`**

### Exemplos:
`$ snap find spotify` → Pesquisa por pacotes Snap relacionados a 'spotify'.

`# snap install spotify` → Instala o pacote Snap chamado 'spotify'.

`$ snap list` → Lista todos os Snaps instalados no sistema.

`# snap refresh` → Atualiza todos os Snaps para suas versões mais recentes.

`# snap remove spotify` → Remove o Snap chamado 'spotify'.

`# snap revert spotify` → Reverte o Snap chamado 'spotify' para a versão anterior.

`$ snap services` → Lista serviços Snap ativos e seu status.