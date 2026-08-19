# Configuração de Área de Trabalho para C++ (WSL 2 ou Ubuntu Nativo)

Guia para montar um ambiente de desenvolvimento C++ moderno (**C++26**) em Linux, tanto via **WSL 2 no Windows** quanto em **Ubuntu 24 nativo**, com compiladores, Visual Studio Code, integração com o GitHub e as bibliotecas ZeroMQ/cppzmq.

Cada passo é marcado com uma etiqueta indicando em qual ambiente ele deve ser executado:

| Etiqueta | Significado |
|---|---|
| **[WSL]** | Executar apenas se você estiver usando WSL 2 no Windows. |
| **[Ubuntu nativo]** | Executar apenas se você estiver em uma instalação Ubuntu nativa. |
| **[Ambos]** | Executar nos dois casos — roda dentro do terminal do Ubuntu, seja ele o do WSL ou o nativo. |

---

## Índice

1. [Visão Geral](#visão-geral)
2. [Escolha do Ambiente](#escolha-do-ambiente)
3. [Pré-requisitos](#pré-requisitos)
4. [Passo 1 — Configurar o WSL 2 [WSL]](#passo-1--configurar-o-wsl-2-wsl)
5. [Passo 2 — Instalar o compilador C++ (C++26) [Ambos]](#passo-2--instalar-o-compilador-c-c26-ambos)
6. [Passo 3 — Instalar e configurar o VS Code](#passo-3--instalar-e-configurar-o-vs-code)
7. [Passo 4 — Configurar chave SSH para o GitHub [Ambos]](#passo-4--configurar-chave-ssh-para-o-github-ambos)
8. [Passo 5 — Configurar Git e área de trabalho [Ambos]](#passo-5--configurar-git-e-área-de-trabalho-ambos)
9. [Passo 6 — Clonar o projeto do GitHub [Ambos]](#passo-6--clonar-o-projeto-do-github-ambos)
10. [Passo 7 — Instalar ZeroMQ e cppzmq [Ambos]](#passo-7--instalar-zeromq-e-cppzmq-ambos)
11. [Passo 8 — Abrir o projeto no VS Code](#passo-8--abrir-o-projeto-no-vs-code)
12. [Notas Adicionais](#notas-adicionais)

---

## Visão Geral

O ambiente final é composto por:

- **Distribuição:** Ubuntu 24.04 (rodando sob WSL 2 no Windows, ou instalado nativamente).
- **Compilador:** GCC com suporte a **C++26** (`-std=c++26`).
- **Editor:** Visual Studio Code, com conexão remota ao WSL (no caso WSL) ou instalado direto no Ubuntu (no caso nativo).
- **Versionamento:** Git com autenticação SSH no GitHub.
- **Bibliotecas:** ZeroMQ (`libzmq`) e o wrapper C++ `cppzmq`.

A maior parte dos comandos é idêntica nos dois ambientes, pois roda **dentro do terminal do Ubuntu**. A diferença concentra-se em dois pontos: a preparação inicial do WSL (Passo 1, exclusivo do WSL) e a instalação do VS Code (Passo 3, com fluxos distintos).

---

## Escolha do Ambiente

| Ambiente | Quando usar | Passos exclusivos |
|---|---|---|
| **WSL 2 (Windows)** | Você usa Windows 10/11 e quer um Linux integrado sem dual boot. | Passo 1 completo; Passo 3 no modo "Windows + Remote". |
| **Ubuntu nativo** | Você já roda Ubuntu 24 diretamente na máquina. | Pula o Passo 1; Passo 3 no modo "Ubuntu nativo". |

> **Nota:** Do Passo 2 em diante, os comandos marcados como **[Ambos]** são executados no terminal do Ubuntu. No WSL, esse é o terminal da distro Ubuntu-24.04 aberta pelo Windows; no nativo, é o terminal padrão do sistema.

---

## Pré-requisitos

**[WSL]**
- Windows 10 ou 11 com suporte a WSL 2 (virtualização habilitada na BIOS/UEFI).

**[Ubuntu nativo]**
- Ubuntu 24.04 já instalado e atualizado.

**[Ambos]**
- Acesso à internet para baixar pacotes e clonar repositórios.
- Conta no GitHub.

---

## Passo 1 — Configurar o WSL 2 [WSL]

> **Nota:** Esta seção é **exclusiva do WSL**. Se você está em Ubuntu nativo, pule direto para o [Passo 2](#passo-2--instalar-o-compilador-c-c26-ambos).

1. Abra o **PowerShell como administrador** e instale o WSL:
   ```powershell
   wsl --install
   ```
2. Garanta que a versão padrão é a 2:
   ```powershell
   wsl --set-default-version 2
   ```
3. Reinicie o computador, se solicitado.
4. Instale o Ubuntu 24.04:
   ```powershell
   wsl --install -d Ubuntu-24.04
   ```
5. Configure o usuário e a senha do Ubuntu quando solicitado.

Após esse passo, abra o terminal do **Ubuntu-24.04** — é nele que todos os comandos **[Ambos]** serão executados.

---

## Passo 2 — Instalar o compilador C++ (C++26) [Ambos]

> **Nota:** Este trecho de instalação do C++26 usa o caminho padrão de "GCC mais recente no Ubuntu" (PPA `ubuntu-toolchain-r/test`). **Confira contra o procedimento que você já rodou na sua máquina** e ajuste a versão do GCC / o método se você tiver usado outro (ex.: `g++-14` direto dos repositórios, ou build do GCC a partir do fonte).

1. Atualize os índices de pacotes:
   ```bash
   sudo apt update
   ```
2. Instale a base de compilação (compilador padrão, debugger, versionador e utilitários):
   ```bash
   sudo apt install -y build-essential gdb git tmux cmake libtool curl
   ```
   - `build-essential` traz `gcc`/`g++`/`make` na versão padrão do Ubuntu 24 (GCC 13), que **não** cobre C++26 por completo. Os passos seguintes adicionam um GCC mais novo.

3. Adicione o PPA com as versões mais recentes do GCC e instale o **g++-15**:
   ```bash
   sudo add-apt-repository -y ppa:ubuntu-toolchain-r/test
   sudo apt update
   sudo apt install -y gcc-15 g++-15
   ```

4. Defina o GCC 15 como padrão do sistema (mantendo `gcc` e `g++` apontando para a mesma versão):
   ```bash
   sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-15 100 \
        --slave /usr/bin/g++ g++ /usr/bin/g++-15
   ```

5. Verifique a versão e teste a compilação com C++26:
   ```bash
   g++ --version
   echo 'int main() { return 0; }' > /tmp/teste26.cpp
   g++ -std=c++26 /tmp/teste26.cpp -o /tmp/teste26 && echo "C++26 OK"
   ```

> **Nota:** Se preferir não usar PPA de terceiros, o Ubuntu 24 traz o **g++-14** direto dos repositórios oficiais (`sudo apt install -y g++-14`), que já aceita `-std=c++26`, porém com suporte à norma menos completo que o do GCC 15.

---

## Passo 3 — Instalar e configurar o VS Code

A instalação difere entre os dois ambientes. Siga **apenas** a subseção correspondente ao seu caso.

### ▸ WSL (Windows + Remote) [WSL]

1. Baixe e instale o Visual Studio Code **no Windows** a partir do [site oficial](https://code.visualstudio.com/).
2. No VS Code, instale a extensão **WSL** (Microsoft).
3. Conecte ao WSL:
   - Clique no botão verde no canto inferior esquerdo (ícone de setas `><`).
   - Selecione **Connect to WSL** e escolha o **Ubuntu-24.04**.
4. Com a janela já conectada ao WSL, instale as extensões **no contexto do WSL** (ver tabela abaixo).

### ▸ Ubuntu nativo [Ubuntu nativo]

1. Instale o VS Code diretamente no Ubuntu. Forma mais simples, via snap:
   ```bash
   sudo snap install --classic code
   ```
   Alternativa via repositório oficial da Microsoft (`apt`):
   ```bash
   sudo apt install -y wget gpg
   wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
   sudo install -D -o root -g root -m 644 packages.microsoft.gpg /etc/apt/keyrings/packages.microsoft.gpg
   echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" \
        | sudo tee /etc/apt/sources.list.d/vscode.list > /dev/null
   rm -f packages.microsoft.gpg
   sudo apt update
   sudo apt install -y code
   ```
2. Abra o VS Code (`code`) e instale as extensões (ver tabela abaixo).

### Extensões (ambos os fluxos)

| Extensão | Utilização |
|---|---|
| **C/C++ Extension Pack** | Suporte a C/C++ (IntelliSense, debug, CMake). |
| **Markdown All in One** | Edição de arquivos Markdown. |
| **Bearded Theme** | Tema visual do editor. |

> **Nota:** No WSL, as extensões precisam ser instaladas **na janela conectada ao WSL**, não apenas no Windows — o VS Code separa extensões "locais" das que rodam no ambiente remoto.

---

## Passo 4 — Configurar chave SSH para o GitHub [Ambos]

Execute no terminal do Ubuntu (WSL ou nativo).

1. Gere uma chave SSH no padrão **ed25519** (recomendado pelo GitHub):
   ```bash
   ssh-keygen -t ed25519 -C "pedroh.s.cravo@gmail.com"
   ```
   - Pressione Enter para aceitar o local padrão (`~/.ssh/id_ed25519`) e defina uma senha (opcional, mas recomendável).
2. Exiba a chave **pública**:
   ```bash
   cat ~/.ssh/id_ed25519.pub
   ```
3. Copie a chave exibida (linha inteira, começando com `ssh-ed25519`).
4. No GitHub:
   - Vá em **Settings > SSH and GPG keys > New SSH key**.
   - Cole a chave e dê um nome (ex.: "WSL Ubuntu" ou "Ubuntu nativo").
   - Salve.
5. Teste a conexão:
   ```bash
   ssh -T git@github.com
   ```

> **Nota:** O guia antigo usava `ssh-keygen -b 1024 -t rsa`. Chaves RSA de 1024 bits são consideradas inseguras e **não são mais aceitas** pelo GitHub — por isso o padrão aqui passou a ser `ed25519`.

---

## Passo 5 — Configurar Git e área de trabalho [Ambos]

1. Crie a pasta do projeto:
   ```bash
   mkdir Ontick && cd Ontick
   ```
2. Configure o Git com suas credenciais:
   ```bash
   git config --global user.name "Pedro Cravo"
   git config --global user.email "pedroh.s.cravo@gmail.com"
   ```

---

## Passo 6 — Clonar o projeto do GitHub [Ambos]

1. No GitHub, acesse o repositório desejado.
2. Clique em **Code > Local > SSH** e copie o link (ex.: `git@github.com:usuario/projeto.git`).
3. No terminal do Ubuntu, clone o repositório:
   ```bash
   git clone -o <nome_do_projeto> <link_ssh_copiado>
   ```
   - Exemplo:
     ```bash
     git clone -o meu_projeto git@github.com:usuario/projeto.git
     ```

---

## Passo 7 — Instalar ZeroMQ e cppzmq [Ambos]

### libzmq (ZeroMQ)

Instalação via `apt`:
```bash
sudo apt install -y libzmq3-dev
```

Caso precise compilar a partir do fonte (versão mais recente ou por segurança):
```bash
git clone git@github.com:zeromq/libzmq.git
cd libzmq && ./autogen.sh && ./configure
make check
sudo make install
sudo ldconfig
cd ..
```

### cppzmq (wrapper C++)

Instalação padrão:
```bash
git clone git@github.com:zeromq/cppzmq.git
cd cppzmq
mkdir build && cd build
cmake -DCPPZMQ_BUILD_TESTS=OFF ..
sudo make -j4 install
sudo ldconfig
cd ../..
```

Alternativa (com cópia manual do header, caso o `install` não coloque o `zmq.hpp` no lugar esperado):
```bash
git clone git@github.com:zeromq/cppzmq.git
cd cppzmq && mkdir build && cd build
cmake -DCPPZMQ_BUILD_TESTS=OFF ..
sudo make -j4 install
sudo ldconfig
cd .. && ./ci_build.sh
sudo cp zmq.hpp /usr/local/include/
cd ..
```

Volte ao diretório do projeto, se necessário:
```bash
cd ~/Ontick
```

---

## Passo 8 — Abrir o projeto no VS Code

**[WSL]** Na janela do VS Code **conectada ao WSL**, vá em **File > Open Folder** e selecione a pasta do projeto (ex.: `Ontick`).

**[Ubuntu nativo]** Abra a pasta direto pelo terminal:
```bash
cd ~/Ontick && code .
```

Depois é só começar a codar.

---

## Notas Adicionais

- **Permissões no WSL:** se houver problemas de permissão, verifique se o usuário tem os acessos corretos usando `sudo`.
- **Atualizar o projeto:** use `git pull` no terminal para trazer as últimas mudanças.
- **Manter o VS Code atualizado:** mantenha o editor e as extensões atualizados para melhor desempenho.
- **Compilar com ZeroMQ em C++26:** inclua o cabeçalho (`#include <zmq.hpp>`) e vincule a biblioteca (`-lzmq`), usando o padrão C++26. Exemplo:
  ```bash
  g++ -std=c++26 seu_arquivo.cpp -lzmq -o seu_programa
  ```
