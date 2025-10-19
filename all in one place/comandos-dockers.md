# 🐳 Comandos Docker - Guia Completo

## 🎯 **Comandos Básicos de Container**

### `docker start <nome|id>`
**Descrição:** Inicia um ou mais containers que estavam parados.
```bash
docker start postgres_payments
docker start container1 container2 container3
```

### `docker stop <nome|id>`
**Descrição:** Para um ou mais containers em execução graciosamente.
```bash
docker stop kafka_broker
docker stop container1 container2
```

### `docker rm <nome|id>`
**Descrição:** Remove um ou mais containers (precisam estar parados).
```bash
docker rm postgres_payments
docker rm container1 container2 container3
```

---

## 💾 **Comandos de Volume**

### `docker volume ls`
**Descrição:** Lista todos os volumes disponíveis no Docker.
```bash
docker volume ls
```

### `docker volume rm <nome|id>`
**Descrição:** Remove um ou mais volumes específicos.
```bash
docker volume rm postgres-data-payments
docker volume rm volume1 volume2
```

### `docker volume prune`
**Descrição:** Remove **todos os volumes não utilizados** por containers.
```bash
docker volume prune
```
**⚠️ Perigoso:** Apaga dados permanentemente!

---

## 🧹 **Comandos de Limpeza em Massa**

### `docker rm $(docker ps -a -q)`
**Descrição:** Remove **todos os containers** (parados e em execução).
```bash
docker rm $(docker ps -a -q)
```
**Equivalente:** `docker container prune`

### `docker stop $(docker ps -q)`
**Descrição:** Para **todos os containers em execução**.
```bash
docker stop $(docker ps -q)
```

---

## 🚀 **Comandos Docker Compose Avançados**

### `docker compose up -d`
**Descrição:** Constrói e inicia os containers em background.
```bash
docker compose up -d
```

### `docker compose up -d --build`
**Descrição:** Constrói as imagens (mesmo sem alterações) e inicia os containers.
```bash
docker compose up -d --build
```
**Quando usar:** Quando fez alterações no Dockerfile ou quer forçar rebuild.

### `docker compose down`
**Descrição:** Para e remove containers, networks criados pelo compose.
```bash
docker compose down
```

### `docker compose down -v`
**Descrição:** Para e remove containers, networks **E VOLUMES**.
```bash
docker compose down -v
```
**⚠️ Cuidado:** Apaga todos os dados dos bancos!

---

## 📊 **Fluxos de Trabalho Comuns**

### 🔄 **Desenvolvimento Diário:**
```bash
# Iniciar
docker compose up -d

# Parar (mantendo dados)
docker compose down

# Reiniciar um serviço específico
docker compose restart postgres
```

### 🧹 **Limpeza Completa:**
```bash
# Parar tudo
docker compose down

# Se quiser limpar dados também
docker compose down -v

# Limpar volumes órfãos
docker volume prune
```

### 🚨 **Emergência - Reset Total:**
```bash
# Parar todos os containers
docker stop $(docker ps -q)

# Remover todos os containers
docker rm $(docker ps -a -q)

# Limpar volumes não utilizados
docker volume prune
```

---

## ⚠️ **Cuidados e Boas Práticas**

### **Comandos Perigosos:**
- `docker compose down -v` → **Perde dados do banco**
- `docker volume prune` → **Perde volumes não usados**
- `docker rm $(docker ps -a -q)` → **Remove TODOS containers**

### **Dicas de Segurança:**
1. Sempre faça backup antes de usar `prune` ou `-v`
2. Use `docker stop` antes de `docker rm`
3. Verifique o que será removido com `ls` antes de `rm`

### **Sequência Segura para Remover:**
```bash
# 1. Parar container
docker stop meu-container

# 2. Verificar se parou
docker ps -a

# 3. Remover container
docker rm meu-container

# 4. Se quiser remover volume também
docker volume rm meu-volume
```

---

## 🎯 **Resumo Visual**

```
🟢 docker start    -> Inicia container parado
🔴 docker stop     -> Para container em execução
🗑️  docker rm      -> Remove container (deve estar parado)
💾 docker volume   -> Gerencia volumes de dados
🧹 docker prune    -> Limpeza geral (cuidado!)
🚀 compose up      -> Sobe toda a aplicação
⏹️  compose down   -> Para aplicação
```

**💡 Lembre-se:** Sempre verifique duas vezes antes de usar comandos de remoção em massa!