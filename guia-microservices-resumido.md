# Guia Completo sobre Microsserviços

## 1. Conceitos Fundamentais

### O que são microsserviços?
- Definição e diferença em relação à arquitetura monolítica.

### Por que usar microsserviços?
- Problemas resolvidos, benefícios (escalabilidade, flexibilidade) e desafios.

### Serviços orientados a domínios
- Relação entre Domain-Driven Design (DDD) e microsserviços.

## 2. Comunicação entre Serviços

### Como os microsserviços se comunicam?
- Protocolos usados: HTTP/REST, gRPC, mensageria (Kafka, RabbitMQ).

### Comunicação síncrona vs. assíncrona
- Quando utilizar cada abordagem.

### API Gateway
- Centraliza requisições e gerencia rotas.

## 3. Gestão de Dados

### Bancos de dados em microsserviços
- Importância de cada serviço ter seu próprio banco.

### Event Sourcing e CQRS
- Consistência de dados em sistemas distribuídos.

### Transações distribuídas
- Uso do Saga Pattern.

## 4. Implantação e DevOps

### Como implantar microsserviços?
- Containers (Docker) e orquestração (Kubernetes).

### CI/CD em microsserviços
- Pipelines eficientes para múltiplos serviços.

### Versionamento de APIs
- Garantia de compatibilidade.

## 5. Escalabilidade e Resiliência

### Escalabilidade
- Horizontal vs. vertical.

### Padrões de resiliência
- Circuit Breaker, Retry, Bulkhead.

### Service Discovery e Load Balancing
- Importância na arquitetura distribuída.

## 6. Segurança

### Segurança entre microsserviços
- Autenticação (JWT, OAuth2) e autorização (RBAC).

### Proteção de APIs e comunicações
- Uso de TLS, mTLS, service mesh (Istio).

## 7. Monitoramento e Observabilidade

### Monitoramento
- Métricas, logs distribuídos (ELK Stack, Grafana Loki) e rastreamento (Jaeger, Zipkin).

### Health Check e Distributed Tracing
- Ferramentas e boas práticas.

## 8. Organização da Equipe

### Estrutura de times
- Conway's Law e times cross-funcionais.

### Ownership de serviços
- Responsabilidades dentro da equipe.

## 9. Migração de Monólito para Microsserviços

### Quando migrar?
- Identificação de sinais de necessidade.

### Estratégias de migração
- Strangler Pattern.

### Gerenciamento de dependências
- Boas práticas.

## 10. Custos e Trade-offs

### Custos operacionais
- Complexidade, infraestrutura, gerenciamento.

### Quando evitar microsserviços?
- Casos em que não são ideais.

## 11. Casos de Uso e Exemplos

### Empresas que usam microsserviços
- Netflix, Amazon, Uber.

### Lições aprendidas
- Erros e soluções aplicadas.

## Recursos para Aprofundamento

### Livros
- "Building Microservices" (Sam Newman), "Microservices Patterns" (Chris Richardson).

### Cursos
- Pluralsight, Udemy, AWS/Google Cloud.

### Prática Hands-on
- Criação de um projeto simples com 2-3 microsserviços (ex: sistema de e-commerce).

