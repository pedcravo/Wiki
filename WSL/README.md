# **WSL**
O Windows Subsystem for Linux (WSL) é uma camada de compatibilidade desenvolvida pela Microsoft que permite rodar distribuições Linux (como Ubuntu, Debian, etc.) diretamente no Windows sem a necessidade de uma máquina virtual tradicional ou dual-boot. Ele integra o Linux ao Windows, permitindo que você execute comandos, ferramentas e scripts Linux em um ambiente nativo, ao lado de aplicativos Windows.

- **WSL 1**: Lançado em 2016, usa uma camada de tradução para converter chamadas do sistema Linux em chamadas do Windows. É mais leve, mas tem limitações (ex.: sem suporte completo ao `systemd`).
- **WSL 2**: Introduzido em 2019, usa uma máquina virtual leve com um kernel Linux real, oferecendo melhor desempenho e suporte completo a recursos como `systemd`. É a versão recomendada hoje.

## **Como funciona?**
O WSL combina o kernel do Windows com um ambiente Linux:
- **WSL 1**: Traduz chamadas de sistema em tempo real, sem um kernel Linux completo.
- **WSL 2**: Executa um kernel Linux real em uma VM otimizada, gerenciada pelo Windows. Ele usa o Hyper-V para virtualização leve e suporta sistemas de arquivos, redes e processos Linux nativos.
- **Integração**: Arquivos do Windows são acessíveis pelo Linux (via `/mnt/c`), e você pode chamar comandos Linux de um terminal Windows (PowerShell/CMD) ou vice-versa.

O WSL 2 também suporta o `systemd` (desde a versão 0.67.6, com configuração adequada), o que é essencial para muitas distribuições modernas, como o Ubuntu 24.04.

## **Como baixar e instalar o WSL?**
1. **Pré-requisitos**:
   - Windows 10 versão 1903 (ou superior) ou Windows 11.
   - Para WSL 2: Windows 10 versão 2004 (build 19041) ou superior.

2. **Instalação básica**:
   - Abra o PowerShell como administrador e execute:
     ```powershell
     wsl --install
     ```
     Isso instala o WSL e o WSL 2 como padrão, além de baixar uma distribuição (geralmente Ubuntu) se nenhuma estiver presente.
   - Reinicie o computador se solicitado.

3. **Instalar uma distribuição específica**:
   - Após instalar o WSL, baixe uma distribuição da Microsoft Store (ex.: Ubuntu 24.04 LTS) ou use:
     ```powershell
     wsl --install -d Ubuntu-24.04
     ```
   - Inicie a distribuição:
     ```powershell
     wsl -d Ubuntu-24.04
     ```
     Na primeira execução, você configura um usuário e senha.

4. **Configurar WSL 2 como padrão (opcional)**:
   ```powershell
   wsl --set-default-version 2
   ```

5. **Verificar a instalação**:
   ```powershell
   wsl -l -v
   ```
   Exemplo de saída:
   ```
     NAME            STATE           VERSION
   * Ubuntu-24.04    Stopped         2
   ```

## **Caso ocorra o erro: `"System has not been booted with systemd"`**
Esse erro ocorre quando uma distribuição Linux espera que o `systemd` seja o sistema de inicialização (PID 1), mas o WSL usa um `init` simplificado por padrão. Veja como corrigir:

### **Sintomas**
- Ao rodar `systemctl`, você vê:
  ```
  System has not been booted with systemd as init system (PID 1). Can't operate.
  Failed to connect to bus: Host is down
  ```
- Durante `sudo apt upgrade`, pode aparecer:
  ```
  Failed to take /etc/passwd lock: Invalid argument
  ```

### **Solução**
1. **Habilitar o systemd**:
   - Edite o arquivo `/etc/wsl.conf` na distribuição:
     ```bash
     sudo nano /etc/wsl.conf
     ```
     Adicione:
     ```
     [boot]
     systemd=true
     ```
     Salve e saia.

2. **Reiniciar o WSL**:
   - No PowerShell:
     ```powershell
     wsl --shutdown
     ```
   - Reabra a distribuição:
     ```powershell
     wsl -d Ubuntu-24.04
     ```

3. **Verificar**:
   - Cheque o PID 1:
     ```bash
     ps -p 1 -o comm=
     ```
     Deve retornar `systemd`. Se ainda for `init`, siga os próximos passos.

4. **Garantir WSL 2**:
   - Confirme a versão:
     ```powershell
     wsl -l -v
     ```
     Se estiver em VERSION 1, converta:
     ```powershell
     wsl --set-version Ubuntu-24.04 2
     ```

5. **Corrigir pacotes quebrados**:
   - Após ativar o `systemd`, repare os pacotes:
     ```bash
     sudo dpkg --configure -a
     sudo apt upgrade
     ```

### **Possíveis problemas**
- **Configuração não aplicada**: Certifique-se de que `/etc/wsl.conf` está correto e reinicie o WSL completamente.
- **Múltiplas distribuições**: Se tiver mais de uma (ex.: `Ubuntu` e `Ubuntu-24.04`), defina a correta como padrão:
  ```powershell
  wsl --set-default Ubuntu-24.04
  ```