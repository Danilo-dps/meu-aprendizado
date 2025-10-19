# Guia para Separar Projetos em Repositórios Individuais

Este guia apresenta métodos para separar projetos independentes que estão no mesmo repositório Git, mantendo o histórico de commits de cada um.

## 📋 Pré-requisitos

- Git instalado
- Acesso aos repositórios no GitHub
- Projetos em pastas separadas no repositório original

## 🔍 Identificar a Estrutura do Repositório

```bash
# Clone o repositório original
git clone https://github.com/seu-usuario/repositorio-original.git
cd repositorio-original

# Liste a estrutura de pastas
ls -la
# ou
tree -d
```

## 🛠️ Método 1: Git Filter-Repo (Recomendado)

### Instalação

**Windows:**
```bash
pip install git-filter-repo
```

**Linux (Ubuntu/Debian):**
```bash
sudo apt update
sudo apt install git-filter-repo
```

**macOS:**
```bash
brew install git-filter-repo
```

### Comandos

```bash
# Para o Projeto 1 (ex: pasta 'pay')
git clone https://github.com/seu-usuario/repositorio-original.git projeto1
cd projeto1
git filter-repo --path pay/
git remote add origin https://github.com/seu-usuario/novo-projeto-pay.git
git push -u origin main

# Para o Projeto 2 (ex: pasta 'api')
git clone https://github.com/seu-usuario/repositorio-original.git projeto2
cd projeto2
git filter-repo --path api/
git remote add origin https://github.com/seu-usuario/novo-projeto-api.git
git push -u origin main
```

**Vantagens:**
- ⚡ Mais rápido e eficiente
- 🎯 Mais controle sobre o filtro
- 🧹 Limpeza automática do histórico

## 🛠️ Método 2: Git Subtree (Nativo - Não Requer Instalação)

### Comandos

```bash
# Para o Projeto 1
git clone https://github.com/seu-usuario/repositorio-original.git projeto1
cd projeto1
git subtree split -P pay -b pay-only
mkdir ../novo-projeto-pay && cd ../novo-projeto-pay
git init
git pull ../projeto1 pay-only
git remote add origin https://github.com/seu-usuario/novo-projeto-pay.git
git push -u origin main

# Para o Projeto 2
git clone https://github.com/seu-usuario/repositorio-original.git projeto2
cd projeto2
git subtree split -P api -b api-only
mkdir ../novo-projeto-api && cd ../novo-projeto-api
git init
git pull ../projeto2 api-only
git remote add origin https://github.com/seu-usuario/novo-projeto-api.git
git push -u origin main
```

**Vantagens:**
- ✅ Não precisa instalar nada
- 🚀 Rápido e eficiente
- 📦 Mantém todo o histórico relevante

## 🛠️ Método 3: Git Filter-Branch (Alternativa Nativa)

### Comandos

```bash
# Para o Projeto 1
git clone https://github.com/seu-usuario/repositorio-original.git projeto1
cd projeto1
git filter-branch --prune-empty --subdirectory-filter pay HEAD
git gc --aggressive --prune=now
git remote set-url origin https://github.com/seu-usuario/novo-projeto-pay.git
git push -u origin main

# Para o Projeto 2
git clone https://github.com/seu-usuario/repositorio-original.git projeto2
cd projeto2
git filter-branch --prune-empty --subdirectory-filter api HEAD
git gc --aggressive --prune=now
git remote set-url origin https://github.com/seu-usuario/novo-projeto-api.git
git push -u origin main
```

**Observações:**
- ⚠️ Mais lento que os outros métodos
- 🏗️ Nativo do Git (não requer instalação extra)
- 🔧 Requer limpeza manual com `git gc`

## 📝 Passo a Passo Completo

1. **Preparação:**
   ```bash
   # Backup do repositório original (opcional)
   git clone https://github.com/seu-usuario/repositorio-original.git backup-original
   ```

2. **Criar repositórios vazios no GitHub:**
   - `novo-projeto-pay`
   - `novo-projeto-api`

3. **Executar um dos métodos acima**

4. **Verificação:**
   ```bash
   # Verificar commits
   git log --oneline
   
   # Verificar arquivos
   ls -la
   
   # Verificar tamanho do repositório
   git count-objects -vH
   ```

## 🎯 Comparação dos Métodos

| Método | Velocidade | Facilidade | Instalação | Recomendação |
|--------|------------|------------|------------|--------------|
| **filter-repo** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | Requer | 🏆 Melhor |
| **subtree** | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | Nativo | 🥈 Excelente |
| **filter-branch** | ⭐⭐ | ⭐⭐⭐ | Nativo | 🥉 Alternativa |

## ❌ Limitações e Cuidados

- **Commits mistos**: Se um commit modifica arquivos de ambos os projetos, ele será duplicado
- **Arquivos raiz**: Arquivos na raiz do repositório original não serão incluídos
- **Backup**: Sempre faça backup antes de operações destrutivas

## ✅ Verificação Final

Após a separação, verifique se:

- [ ] Cada repositório contém apenas os arquivos do projeto específico
- [ ] O histórico de commits está preservado
- [ ] Todos os branches importantes foram migrados
- [ ] Os repositórios novos estão funcionando corretamente

## 🆘 Solução de Problemas

### Erro "command not found" para filter-repo:
```bash
# Adicionar ao PATH (Linux/macOS)
export PATH=$PATH:$(python -m site --user-base)/bin

# Ou usar método alternativo (subtree)
```

### Erro de permissão no push:
```bash
# Verificar remotes
git remote -v

# Configurar credenciais
git config --global user.name "Seu Nome"
git config --global user.email "seu@email.com"
```

---

**Recomendação**: Use o **Método 2 (git subtree)** para simplicidade ou **Método 1 (git filter-repo)** para máximo controle.