## 1. `sudo`

### Para que serve?
O comando `sudo` é utilizado para **executar comandos como superusuário (root) ou como outro usuário**, sem a necessidade de trocar de sessão.

O `sudo` (SUperuser DO) permite a usuários autorizados executar comandos com privilégios elevados, fornecendo a senha do próprio usuário (em vez da senha do root). É frequentemente usado para realizar tarefas administrativas temporariamente, sem a necessidade de logar como root.

---

### Opções:
- `-i` → Abre um shell de login como root, carregando o ambiente de login completo (similar ao `su -`).
- `-k` → Invalida o cache de autenticação do sudo, forçando o próximo comando sudo a pedir a senha novamente (contrário do `-v`).
- `-l` → Lista os comandos que o usuário atual tem permissão para executar com `sudo`.
- `-s` → Inicia um shell interativo como root ou outro usuário.
- `-u` → Especifica o usuário com o qual o comando será executado (por padrão, o usuário é o root).
- `-v` → Revalida a autenticação sudo sem executar nenhum comando, pedindo a senha novamente para estender o período de autenticação (contrário do `-k`).

---

### Sintaxe comum:
`$ sudo [OPÇÕES] COMANDO`

Exemplos
````bash
$ sudo apt update                        # Executa o comando apt como root
$ sudo -u pedro mkdir diretorio          # Executa o comando mkdir como usuário "pedro"
$ sudo -l                                # Exibe uma lista de comandos permitidos para o usuário atual, de acordo com o arquivo /etc/sudoers
````

---

### Arquivo `Makefile`

Este Makefile combina `TrocaDeUsuario.md` e `sudo.md` em um único arquivo `README.md`, substituindo `<!-- INCLUDE sudo.md HERE -->` pelo conteúdo de `sudo.md`:

```makefile
README.md: TrocaDeUsuario.md sudo.md
	echo "Criando README.md com conteúdo de TrocaDeUsuario.md e sudo.md..."
	cat TrocaDeUsuario.md | sed '/<!-- INCLUDE sudo.md HERE -->/r sudo.md' > README.md
	echo "README.md atualizado com sucesso!"
