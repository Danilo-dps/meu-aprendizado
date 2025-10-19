# Guia para Lidar com Conflitos de Merge no Git

## O que são Conflitos de Merge?

Conflitos ocorrem quando o Git não pode automaticamente resolver diferenças entre branches durante um merge. Isso geralmente acontece quando:

- Duas branches modificam a mesma linha de um arquivo
- Um arquivo é modificado em uma branch e deletado em outra
- Alterações incompatíveis no mesmo código

## Fluxo para Prevenir Conflitos

### 1. Mantenha sua Branch Atualizada
```bash
# Na sua branch de feature
git checkout main
git pull origin main
git checkout minha-feature
git merge main
# Ou use rebase para histórico mais limpo
git rebase main
```

### 2. Commits Frequentes e Pequenos
```bash
# Em vez de um commit grande
git add .
git commit -m "muitas alterações"

# Faça commits menores e específicos
git add arquivo1.js
git commit -m "feat: adiciona funcionalidade X"
git add arquivo2.js
git commit -m "fix: corrige bug no componente Y"
```

## Resolvendo Conflitos Passo a Passo

### Cenário 1: Merge com Conflitos

```bash
# Tentando fazer merge da main na feature branch
git checkout minha-feature
git merge main

# Saída esperada:
# Auto-merging arquivo.js
# CONFLICT (content): Merge conflict in arquivo.js
# Automatic merge failed; fix conflicts and then commit the result.
```

### 2. Identificar Arquivos em Conflito
```bash
git status
# Saída:
# Unmerged paths:
#   both modified:   arquivo.js
#   both modified:   estilo.css
```

### 3. Analisar os Conflitos

Os arquivos em conflito terão marcadores especiais:

```javascript
// arquivo.js
<<<<<<< HEAD
// Suas alterações na branch atual
console.log("Minha versão da feature");
=======
// Alterações da branch que está sendo mergeada
console.log("Versão da main branch");
>>>>>>> main
```

### 4. Resolver Manualmente os Conflitos

Edite o arquivo e decida qual versão manter:

**Opção A: Manter sua versão**
```javascript
// arquivo.js (após resolver)
console.log("Minha versão da feature");
```

**Opção B: Manter a versão do merge**
```javascript
// arquivo.js (após resolver)
console.log("Versão da main branch");
```

**Opção C: Combinar ambas**
```javascript
// arquivo.js (após resolver)
console.log("Minha versão da feature");
console.log("Versão da main branch");
```

**Opção D: Escrever algo completamente novo**
```javascript
// arquivo.js (após resolver)
console.log("Nova versão combinada");
```

### 5. Marcar Conflito como Resolvido
```bash
# Adicionar cada arquivo resolvido
git add arquivo.js
git add estilo.css

# Ou adicionar todos os arquivos resolvidos
git add .
```

### 6. Completar o Merge
```bash
git commit -m "Merge branch 'main' into minha-feature, resolvendo conflitos"

# Ou se usou git merge --no-commit
git commit
```

## Ferramentas para Resolução de Conflitos

### Usando Ferramentas Visuais
```bash
git mergetool                    # Abre ferramenta gráfica padrão
git mergetool --tool=vimdiff    # Especificar ferramenta
```

### Ferramentas Populares:
- **VS Code**: `code --wait`
- **Meld**: `git mergetool --tool=meld`
- **KDiff3**: `git mergetool --tool=kdiff3`

## Estratégias Avançadas

### 1. Usando Rebase em vez de Merge
```bash
git checkout minha-feature
git rebase main

# Se houver conflitos durante rebase:
# - Resolva os conflitos
# - git add <arquivos>
# - git rebase --continue
# - Se quiser cancelar: git rebase --abort
```

### 2. Merge com Estratégia Específica
```bash
# Preferir alterações da branch atual
git merge -X ours main

# Preferir alterações da branch sendo mergeada
git merge -X theirs main
```

### 3. Abortar Merge em Andamento
```bash
# Se você começou um merge e quer cancelar
git merge --abort

# Para rebase
git rebase --abort
```

## Comandos Úteis para Debug

### Ver Diferentes entre Branches
```bash
# Ver diferenças entre branches
git diff minha-feature main

# Ver o que será mergeado
git log --oneline main..minha-feature
git log --oneline minha-feature..main
```

### Ver Histórico de Merge
```bash
git log --oneline --graph --all
```

## Fluxo de Trabalho Recomendado

### Para Feature Branches:
```bash
# 1. Comece da main atualizada
git checkout main
git pull origin main

# 2. Crie e trabalhe na feature branch
git checkout -b feature/nova-funcionalidade
# ... faça commits ...

# 3. Atualize com a main regularmente
git fetch origin
git merge origin/main
# OU
git rebase origin/main

# 4. Quando pronto, faça merge na main
git checkout main
git merge feature/nova-funcionalidade
```

### Para Hotfixes:
```bash
# 1. Crie da main
git checkout main
git pull origin main
git checkout -b hotfix/urgente

# 2. Faça o fix e commit
# ... correções ...

# 3. Merge rápido para main
git checkout main
git merge hotfix/urgente
git push origin main
```

## Dicas para Evitar Conflitos

### 1. Comunicação
- Avise a equipe quando for trabalhar em arquivos compartilhados
- Use revisão de código (code review)

### 2. Organização do Código
- Mantenha funções pequenas e específicas
- Use arquivos separados para funcionalidades diferentes

### 3. Práticas de Desenvolvimento
- Pull requests pequenos e frequentes
- Testes automatizados
- Integração contínua

### 4. Convenções de Equipe
```bash
# Padrão de commits semânticos
feat: nova funcionalidade
fix: correção de bug
docs: documentação
style: formatação
refactor: refatoração
test: testes
```

## Exemplo Prático Completo

```bash
# Situação: Conflito em arquivo de configuração
git checkout minha-feature
git merge main

# Identificar conflitos
git status

# Editar arquivo config.json
{
  "apiUrl": "<<<<<<< HEAD",
  "apiUrl": "https://minha-api.com",
  "=======",
  "apiUrl": "https://api-producao.com",
  ">>>>>>> main",
  "timeout": 5000
}

# Resolver mantendo a versão de produção
{
  "apiUrl": "https://api-producao.com",
  "timeout": 5000
}

# Finalizar
git add config.json
git commit -m "Merge main into minha-feature, usando apiUrl de produção"
```

Lembre-se: Conflitos são normais no desenvolvimento colaborativo. A chave é resolvê-los de forma sistemática e comunicar com a equipe!