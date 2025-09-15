# Configuração de Área de Trabalho no Windows com WSL

Este guia descreve como configurar uma área de trabalho no Windows utilizando WSL 2, Ubuntu 24, compiladores C++, Visual Studio Code e integração com GitHub.

## Pré-requisitos
- Sistema operacional Windows 10 ou 11 (com suporte ao WSL 2).
- Acesso à internet para baixar pacotes e clonar repositórios.
- Conta no GitHub.

## Passo a passo

### 1. Configurar o WSL 2
1. Abra o PowerShell como administrador e instale o WSL 2:
   ```
   wsl --install
   ```
2. Reinicie o computador, se necessário.
3. Instale o Ubuntu 24 no WSL:
   ```
   wsl --install -d Ubuntu-24.04
   ```
4. Configure o usuário e senha do Ubuntu quando solicitado.

### 2. Instalar compiladores C++ no Ubuntu
1. Abra o terminal do Ubuntu (via WSL).
2. Atualize os pacotes:
   ```
   sudo apt update
   ```
3. Instale o compilador **g++**, debugger **gdb** e versionador de arquivos **git**:
   ```
   sudo apt install g++ gdb git tmux cmake -y
   ```

### 3. Instalar e configurar o Visual Studio Code
1. Baixe e instale o Visual Studio Code no Windows a partir do [site oficial](https://code.visualstudio.com/).
2. Abra o VS Code e conecte ao WSL:
   - Clique no botão inferior esquerdo (ícone de setas, de baixo da engrenagem).
   - Selecione **Connect to WSL** e escolha o Ubuntu-24.04.
3. Instale as seguintes extensões no VS Code (tanto no Windows quanto no WSL):
   - **C/C++ Extension Pack**: Para suporte a C/C++.
   - **Markdown All in One**: Para edição de Markdown.
   - **Bearded Theme**: Tema visual para o VS Code.

### 4. Configurar chave SSH para o GitHub
1. No terminal do Ubuntu (WSL), gere uma chave SSH:
   ```
   ssh-keygen -b 1024 -t rsa
   ```
   - Pressione Enter para aceitar o local padrão (`~/.ssh/id_rsa`) e deixe a senha em branco, se desejar.
2. Exiba a chave pública:
   ```
   cat ~/.ssh/id_rsa.pub
   ```
3. Copie a chave exibida.
4. Acesse o GitHub:
   - Vá para **Settings > SSH and GPG keys > New SSH key** (ou **Add SSH key**).
   - Cole a chave copiada e dê um nome (ex.: "WSL Ubuntu").
   - Salve.

### 5. Configurar área de trabalho
1. No terminal do Ubuntu, crie uma pasta para o projeto:
   ```
   mkdir Ontick && cd Ontick
   ```
2. Configure o Git com suas credenciais:
   ```
   git config --global user.name "Pedro Cravo"
   git config --global user.email "pedroh.s.cravo@gmail.com"
   ```

### 6. Clonar o projeto do GitHub
1. No GitHub, acesse o repositório desejado.
2. Clique em **Code > Local > SSH** e copie o link (ex.: `git@github.com:usuario/projeto.git`).
3. No terminal do Ubuntu, clone o repositório:
   ```
   git clone -o <nome_do_projeto> <link_ssh_copiado>
   ```
   - Exemplo: `git clone -o meu_projeto git@github.com:usuario/projeto.git`

### 7. Instalar bibliotecas ZeroMQ e cppzmq
1. Instale a biblioteca **libzmq** (ZeroMQ):
   ```
   sudo apt install libzmq3-dev
   ```
   - Por via das duvidas faça:
   ```
    git clone git@github.com:zeromq/libzmq.git
    cd libzmq && ./autogen.sh && ./configure
    make check
    sudo make install
    sudo ldconfig
    ```
   
2. Instale a biblioteca **cppzmq** (wrapper C++ para ZeroMQ):
   ```
   git clone git@github.com:zeromq/cppzmq.git
   cd cppzmq
   mkdir build
   cd build
   cmake -DCPPZMQ_BUILD_TESTS=OFF ..
   sudo make -j4 install
   ```
   - Ou faça:
   ```
    git clone git@github.com:zeromq/cppzmq.git
    cd cppzmq && mkdir build && cd build
    cmake -DCPPZMQ_BUILD_TESTS=OFF ..
    sudo make -j4 install
    sudo ldconfig
    cd .. && ./ci_build.sh
    sudo cp zmq.hpp /usr/local/include/
   ```
   
3. Volte ao diretório do projeto (se necessário):
   ```
   cd ~/Ontick
   ```

### 8. Abrir a área de trabalho no VS Code
1. No VS Code, vá até **File > Open Folder**.
2. Selecione a pasta de trabalho (ex.: `Ontick`).
3. Comece a codar.

## Notas adicionais
- Caso encontre problemas com permissões no WSL, verifique se o usuário tem as permissões corretas usando `sudo`.
- Para atualizar o projeto, use comandos como `git pull` no terminal.
- Mantenha o VS Code e as extensões atualizadas para melhor desempenho.
- Para projetos que utilizam ZeroMQ/cppzmq, certifique-se de incluir os cabeçalhos (`#include <zmq.hpp>`) e vincular as bibliotecas (`-lzmq`) ao compilar (ex.: `g++ seu_arquivo.cpp -lzmq -o seu_programa`).
