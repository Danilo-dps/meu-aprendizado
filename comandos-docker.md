docker images para ver o que já tenho
docker ps para ver o que está rodando
docker ps -a é para ?

e para iniciar os conteineres?

# Conferir se está limpo

Após realizar a limpeza, você pode conferir se ainda sobrou algo no Docker com os seguintes comandos:

## Containers:
```sh
docker ps -a
```

## Imagens:
```sh
docker images
```

## Volumes:
```sh
docker volume ls
```

## Redes:
```sh
docker network ls
```

# Guia Prático de Docker

## 1. Imagem (Image)

### O que é?
Uma imagem é como uma "classe" ou um "template". Ela contém tudo o que é necessário para executar um aplicativo (código, bibliotecas, dependências, etc.), mas não está em execução.

### Analogia
Pense em uma imagem como um instalador de software (exemplo: um arquivo `.exe` ou `.iso`). Ele contém tudo o que você precisa, mas não está rodando até que você o execute.

### Comando para visualizar imagens
```bash
docker images
```
**Saída:**
```
REPOSITORY   TAG       IMAGE ID       CREATED        SIZE
nginx        latest    1a5a5a5a5a5a   2 weeks ago    133MB
```

---

## 2. Contêiner (Container)

### O que é?
Um contêiner é uma instância em execução de uma imagem. É como um "objeto" criado a partir da "classe" (imagem). Ele está ativo e consumindo recursos do sistema.

### Analogia
Pense em um contêiner como um processo em execução. Ele é a "instância viva" da imagem.

### Comandos para visualizar contêineres
- **Ver contêineres em execução:**
  ```bash
  docker ps
  ```
  **Saída:**
  ```
  CONTAINER ID   IMAGE     COMMAND                  CREATED        STATUS        PORTS     NAMES
  a1b2c3d4e5f6   nginx     "/docker-entrypoint.…"   5 minutes ago  Up 5 minutes  80/tcp    meu-container
  ```

- **Ver todos os contêineres (ativos e inativos):**
  ```bash
  docker ps -a
  ```

---

## 3. Rede (Network)

### O que é?
Uma rede Docker é um ambiente virtual que permite a comunicação entre contêineres. Ela pode ser usada para isolar contêineres ou conectá-los entre si.

### Analogia
Pense em uma rede como um "grupo de WhatsApp". Os contêineres são os participantes do grupo, e a rede é o meio que permite que eles se comuniquem.

### Comando para visualizar redes
```bash
docker network ls
```
**Saída:**
```
NETWORK ID     NAME          DRIVER    SCOPE
1a2b3c4d5e6f   bridge        bridge    local
7g8h9i0j1k2l   minha-rede    bridge    local
```

---

## Como tudo se conecta

1. **Imagem:** Você baixa ou cria uma imagem (exemplo: nginx).
2. **Contêiner:** Você cria e inicia um contêiner a partir dessa imagem:
   ```bash
   docker run -d --name meu-container nginx
   ```
3. **Rede:** Você conecta o contêiner a uma rede:
   ```bash
   docker network connect minha-rede meu-container
   ```

---

## Comandos para monitoramento

- **Ver imagens disponíveis:**
  ```bash
  docker images
  ```

- **Ver contêineres em execução:**
  ```bash
  docker ps
  ```

- **Ver todos os contêineres (ativos e inativos):**
  ```bash
  docker ps -a
  ```

- **Ver redes disponíveis:**
  ```bash
  docker network ls
  ```

- **Inspecionar uma rede específica:**
  ```bash
  docker network inspect minha-rede
  ```

---

## Exemplo Prático

### 1. Criar uma rede
```bash
docker network create minha-rede
```

### 2. Executar um contêiner conectado à rede
```bash
docker run -d --name meu-container --network minha-rede nginx
```

### 3. Verificar o contêiner em execução
```bash
docker ps
```

### 4. Verificar a rede e os contêineres conectados
```bash
docker network inspect minha-rede
```

---

## Resumo

- **Imagem:** Template (não está rodando).
- **Contêiner:** Instância em execução da imagem.
- **Rede:** Meio de comunicação entre contêineres.


