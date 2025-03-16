# Comandos Básicos do Linux

Uma rápida referência para alguns comandos básicos usados frequentemente no sistema operacional Linux.

## Navegação

- `pwd`: Exibe o diretório de trabalho atual.
- `ls`: Lista os arquivos e diretórios no diretório atual.
- `cd [diretório]`: Muda para o diretório especificado.

## Manipulação de Arquivos e Diretórios

- `cp [origem] [destino]`: Copia arquivos ou diretórios.
- `mv [origem] [destino]`: Move ou renomeia arquivos ou diretórios.
- `rm [arquivo]`: Remove arquivos.
- `mkdir [diretório]`: Cria um novo diretório.
- `rmdir [diretório]`: Remove um diretório vazio.

## Visualização e Edição de Arquivos

- `cat [arquivo]`: Exibe o conteúdo de um arquivo.
- `nano [arquivo]`: Abre o editor de texto Nano para editar um arquivo.
- `vim [arquivo]`: Abre o editor de texto Vim para editar um arquivo.
- `less [arquivo]`: Exibe o conteúdo de um arquivo uma página de cada vez.

## Permissões

- `chmod [opções] [arquivo]`: Modifica as permissões de um arquivo ou diretório.
- `chown [usuário:grupo] [arquivo]`: Altera o proprietário de um arquivo ou diretório.

## Processos

- `ps`: Exibe uma lista de processos em execução.
- `top`: Monitora os processos em tempo real.
- `kill [pid]`: Termina um processo usando o ID do processo (PID).
- `pkill [nome]`: Termina um processo pelo nome.
- `systemctl list-units --type=service --state=running`: para ver serviços que estão ativos

## Rede

- `ping [endereço]`: Envia pacotes ICMP para verificar a conectividade com um host.
- `ifconfig`: Exibe e configura interfaces de rede.
- `wget [URL]`: Baixa arquivos da web.

## Outros Comandos Úteis

- `man [comando]`: Exibe o manual do comando especificado.
- `echo [mensagem]`: Exibe uma mensagem no terminal.
- `history`: Exibe o histórico de comandos digitados.

# Limpeza do Sistema Linux

## Comandos para Limpeza e Manutenção

  sudo apt-get clean  # Remove pacotes .deb armazenados em cache que não são mais necessários.
  sudo apt-get autoclean # Remove apenas os pacotes .deb em cache que não são mais possíveis de serem baixados.
  sudo apt-get autoremove # Remove pacotes instalados automaticamente que não são mais necessários.
  sudo rm -rf /var/cache/apt/archives/*.deb # Remove manualmente todos os pacotes .deb em cache.
- sudo apt-get purge [pacote] # Remove um pacote e seus arquivos de configuração.
- sudo du -sh /var/cache/apt # Mostra o espaço usado pelos pacotes em cache.

## Limpeza de Logs

- `sudo journalctl --vacuum-time=2weeks`: Remove logs do sistema mais antigos que duas semanas.
- `sudo rm -rf /var/log/*.log`: Remove todos os arquivos de log no diretório /var/log.

## Outros Comandos Úteis

- `sudo find / -name "*~" -exec rm {} \;`: Encontra e remove arquivos temporários que terminam com ~.
- `sudo find / -name "*.bak" -exec rm {} \;`: Encontra e remove arquivos de backup que terminam com .bak.
- `sudo find / -type f -name ".DS_Store" -delete`: Remove arquivos .DS_Store (usados pelo macOS).

# Diferença entre `su` e `sudo`

## `su`
- **Significado**: Abreviação de "substitute user" ou "switch user".
- **Função**: Permite que um usuário substitua o ambiente de shell por outro usuário, mais frequentemente o usuário root.
- **Comando**: Executando `su` sem especificar um usuário, você assume o papel de root. Por exemplo, `su -` troca para o superusuário (root), exigindo a senha do root.
- **Utilização**:
  - Entrar no ambiente completo do novo usuário, incluindo variáveis de ambiente, diretório inicial, etc.
  - Necessário conhecer a senha do usuário que você está tentando se tornar.
  - Exemplo:
    ```sh
    su - username
    su -
    ```

## `sudo`
- **Significado**: Abreviação de "superuser do" ou "substitute user do".
- **Função**: Executa comandos com privilégios de superusuário (root) sem trocar o ambiente de shell, baseando-se nas permissões configuradas no arquivo `/etc/sudoers`.
- **Comando**: `sudo` seguido do comando que se deseja executar com privilégios elevados. Exemplo, `sudo apt-get update` executa o comando `apt-get update` como root.
- **Utilização**:
  - Executar comandos individuais com permissões elevadas.
  - Não requer a senha do root, mas a senha do usuário atual (se o mesmo estiver listado no `/etc/sudoers`).
  - A configuração pode restringir comandos específicos que podem ser executados por diferentes usuários.
  - Exemplo:
    ```sh
    sudo apt-get update
    sudo systemctl restart apache2
    ```

## Resumo
- **`su`**: Troca o ambiente do shell para outro usuário, mais frequentemente para root, exigindo a senha desse usuário.
- **`sudo`**: Executa comandos com privilégios elevados, requerendo a senha do próprio usuário, baseado em configurações do `/etc/sudoers`.



