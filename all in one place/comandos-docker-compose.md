# 🐳 Comandos Docker Compose - Guia de Referência

## 🚀 Comandos para Iniciar Serviços

### `docker compose up`
**Descrição:** Inicia todos os serviços definidos no arquivo docker-compose.yml no modo foreground (terminal travado).

**Uso:**
```bash
docker compose up
```
**Quando usar:** Para desenvolvimento, quando você quer ver os logs em tempo real.

---

### `docker compose up -d`
**Descrição:** Inicia todos os serviços em background (detached mode).

**Uso:**
```bash
docker compose up -d
```
**Quando usar:** Para produção ou quando quer usar o terminal enquanto os serviços rodam.

---

### `docker compose -f arquivo.yml up -d`
**Descrição:** Inicia serviços usando um arquivo YAML específico.

**Uso:**
```bash
docker compose -f docker-compose-payments.yml up -d
```
**Quando usar:** Quando o arquivo não se chama `docker-compose.yml`.

---

## 📊 Comandos de Monitoramento

### `docker compose ps`
**Descrição:** Lista todos os serviços e seu status atual.

**Uso:**
```bash
docker compose ps
```
**Saída exemplo:**
```
Name                          Command              State           Ports
----------------------------------------------------------------------------
kafka_broker_payments        /docker-entrypoint.sh ...   Up      0.0.0.0:9092->9092/tcp
postgres_payments            docker-entrypoint.sh postgres Up    0.0.0.0:5433->5432/tcp
```

---

### `docker compose logs`
**Descrição:** Mostra os logs de todos os serviços.

**Uso:**
```bash
docker compose logs
```

---

### `docker compose logs [serviço]`
**Descrição:** Mostra logs de um serviço específico.

**Uso:**
```bash
docker compose logs kafka
docker compose logs postgres
```
**Quando usar:** Para debug de um serviço específico.

---

## ⏹️ Comandos para Parar Serviços

### `docker compose down`
**Descrição:** Para e remove todos os containers, networks criados pelo compose.

**Uso:**
```bash
docker compose down
```
**Observação:** Mantém os volumes (dados preservados).

---

### `docker compose down -v`
**Descrição:** Para e remove containers, networks **E volumes**.

**Uso:**
```bash
docker compose down -v
```
**⚠️ Cuidado:** Remove todos os dados do banco e volumes permanentes.

---

## 🔧 Comandos de Gerenciamento

### `docker compose start`
**Descrição:** Inicia serviços já criados mas parados.

**Uso:**
```bash
docker compose start
```

---

### `docker compose stop`
**Descrição:** Para serviços sem removê-los.

**Uso:**
```bash
docker-compose stop
```

---

### `docker compose restart`
**Descrição:** Reinicia todos os serviços.

**Uso:**
```bash
docker compose restart
```

---

### `docker compose restart [serviço]`
**Descrição:** Reinicia um serviço específico.

**Uso:**
```bash
docker compose restart kafka
```

---

## 📋 Comandos de Informação

### `docker compose images`
**Descrição:** Lista as imagens usadas pelos serviços.

**Uso:**
```bash
docker compose images
```

---

### `docker compose top`
**Descrição:** Mostra processos rodando nos containers.

**Uso:**
```bash
docker compose top
```

---

## 🛠️ Fluxo de Trabalho Típico

```bash
# 1. Iniciar serviços
docker compose up -d

# 2. Verificar status
docker compose ps

# 3. Ver logs se necessário
docker compose logs kafka

# 4. Parar serviços (mantendo dados)
docker compose down

# 5. Parar e limpar tudo (dados incluídos)
docker compose down -v
```

## 💡 Dicas Importantes

- Use `-d` para não travar o terminal
- Use `docker compose down` regularmente para limpar
- Use `-v` apenas quando quiser apagar todos os dados
- Sempre verifique o status com `docker-compose ps` após subir os serviços

---