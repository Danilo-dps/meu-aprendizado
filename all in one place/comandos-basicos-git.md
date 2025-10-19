# Comandos Básicos do Git

## Configuração Inicial

### Configurar usuário
```bash
git config --global user.name "Seu Nome"
git config --global user.email "seu.email@exemplo.com"
```

### Verificar configurações
```bash
git config --list
```

## Iniciando um Repositório

### Criar novo repositório
```bash
git init
```

### Clonar repositório existente
```bash
git clone https://github.com/usuario/repositorio.git
```

## Trabalhando com Alterações

### Verificar status do repositório
```bash
git status
```

### Adicionar arquivos para staging
```bash
git add arquivo.txt          # Arquivo específico
git add .                    # Todos os arquivos
git add *.js                 # Todos arquivos .js
```

### Commitar alterações
```bash
git commit -m "Mensagem do commit"
```

### Adicionar e commitar em um comando
```bash
git commit -am "Mensagem do commit"
```

## Histórico e Diferenças

### Ver histórico de commits
```bash
git log
git log --oneline           # Formato resumido
git log --graph             Com gráfico de branches
```

### Ver diferenças
```bash
git diff                    # Alterações não staged
git diff --staged           # Alterações staged
git diff HEAD               # Todas as alterações
```

## Branches (Ramificações)

### Trabalhando com branches
```bash
git branch                  # Listar branches
git branch nova-branch      # Criar nova branch
git checkout nome-branch    # Mudar para branch
git checkout -b nova-branch # Criar e mudar para branch
git branch -d nome-branch   # Deletar branch
```

## Atualizando e Compartilhando

### Baixar alterações do repositório remoto
```bash
git pull origin main
```

### Enviar alterações para o repositório remoto
```bash
git push origin main
```

### Buscar alterações sem aplicar
```bash
git fetch origin
```

## Desfazendo Coisas

### Corrigir último commit (amend)
```bash
git commit --amend -m "Nova mensagem"
```

### Desfazer arquivos do staging
```bash
git reset arquivo.txt
```

### Desfazer alterações locais
```bash
git checkout -- arquivo.txt
```

### Reverter um commit
```bash
git revert <hash-do-commit>
```

## Trabalhando com Remotos

### Adicionar repositório remoto
```bash
git remote add origin https://github.com/usuario/repo.git
```

### Ver repositórios remotos
```bash
git remote -v
```

### Atualizar branch local com remoto
```bash
git pull --rebase origin main
```

## Comandos Úteis do Dia a Dia

### Ver alterações específicas de um arquivo
```bash
git log -p arquivo.txt
```

### Ver quem modificou uma linha
```bash
git blame arquivo.txt
```

### Guardar alterações temporariamente
```bash
git stash                    # Guardar alterações
git stash pop               # Recuperar alterações
git stash list              # Listar stashes
```

### Limpar arquivos não rastreados
```bash
git clean -fd
```

## Fluxo Básico de Trabalho

```bash
# 1. Atualizar repositório local
git pull origin main

# 2. Fazer alterações nos arquivos
# 3. Verificar status
git status

# 4. Adicionar arquivos alterados
git add .

# 5. Fazer commit
git commit -m "Descrição das alterações"

# 6. Enviar para repositório remoto
git push origin main
```

## Dicas Importantes

- Sempre use `git status` para verificar o estado do repositório
- Commits frequentes com mensagens descritivas
- Faça `git pull` antes de `git push` para evitar conflitos
- Use branches para novas funcionalidades
- Teste as alterações antes de commitar

Este arquivo cobre os comandos mais essenciais do Git para o dia a dia de desenvolvimento!