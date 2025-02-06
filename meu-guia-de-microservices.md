# Guia de Microsserviços

## 1. Conceitos Fundamentais
### O que são microsserviços?
Microsserviços são uma abordagem de arquitetura de software onde uma aplicação é dividida em pequenos serviços independentes, cada um responsável por uma funcionalidade específica. Cada serviço roda em seu próprio processo e se comunica com outros serviços através de APIs leves, geralmente usando HTTP/REST ou mensageria.

### Como eles diferem de uma arquitetura monolítica?
Em uma arquitetura monolítica, toda a aplicação é desenvolvida como um único bloco, com todos os módulos e funcionalidades acoplados. Já os microsserviços são desacoplados, permitindo que cada serviço seja desenvolvido, implantado e escalado independentemente.

### Por que usar microsserviços?
- **Escalabilidade:** Cada serviço pode ser escalado individualmente conforme a demanda.
- **Flexibilidade:** Diferentes tecnologias podem ser usadas para cada serviço.
- **Resiliência:** Falhas em um serviço não afetam necessariamente outros.
- **Manutenção:** Facilita a manutenção e atualizações contínuas.

### Quais problemas eles resolvem?
- Dificuldade de escalar aplicações monolíticas.
- Complexidade de manter e atualizar sistemas grandes e acoplados.
- Lentidão no ciclo de desenvolvimento devido ao acoplamento.

### Benefícios e desafios:
- **Benefícios:** Escalabilidade, flexibilidade, resiliência, deploy independente.
- **Desafios:** Complexidade de gerenciamento, latência na comunicação, consistência de dados distribuídos.

### Qual é o princípio de "serviços orientados a domínios"?
É a ideia de que os serviços devem ser projetados em torno de domínios de negócio específicos, refletindo as regras e necessidades do negócio.

### Como o Domain-Driven Design (DDD) se relaciona com microsserviços?
O DDD ajuda a identificar os limites contextuais (Bounded Contexts) que podem se tornar microsserviços. Ele fornece uma estrutura para modelar serviços de forma alinhada ao domínio do negócio.

## 2. Comunicação entre Serviços
### Como os microsserviços se comunicam?
Através de APIs (HTTP/REST, gRPC) ou mensageria (Kafka, RabbitMQ).

### Quais protocolos são usados?
- **HTTP/REST:** Leve e amplamente adotado.
- **gRPC:** Mais eficiente para comunicação interna.
- **Mensageria (Kafka, RabbitMQ):** Para comunicação assíncrona.

### Qual a diferença entre comunicação síncrona e assíncrona?
- **Síncrona:** O cliente espera uma resposta imediata (ex: HTTP/REST).
- **Assíncrona:** O cliente não espera uma resposta imediata (ex: mensageria).

### Quando usar cada uma?
- **Síncrona:** Quando a resposta é necessária imediatamente.
- **Assíncrona:** Para operações demoradas ou quando a disponibilidade do receptor é incerta.

### O que é um API Gateway?
Um ponto único de entrada que centraliza e gerencia requisições para múltiplos microsserviços, lidando com roteamento, autenticação e balanceamento de carga.

## 3. Gestão de Dados
### Como lidar com bancos de dados em microsserviços?
Cada microsserviço deve ter seu próprio banco de dados para garantir independência e evitar acoplamento.

### Por que cada serviço deve ter seu próprio banco de dados?
Para evitar dependências diretas entre serviços e permitir evolução independente.

### O que é Event Sourcing e CQRS?
- **Event Sourcing:** Armazena o estado de uma entidade como uma sequência de eventos.
- **CQRS (Command Query Responsibility Segregation):** Separa operações de leitura e escrita em modelos diferentes.

### Como garantem consistência de dados em sistemas distribuídos?
Através de eventos e replicação assíncrona, garantindo que os dados eventualmente se tornem consistentes.

### Como resolver transações distribuídas (ex: Saga Pattern)?
O padrão Saga divide uma transação em múltiplas etapas, onde cada etapa é compensada em caso de falha.

## 4. Implantação e DevOps
### Como implantar microsserviços?
Usando containers (Docker) e orquestração (Kubernetes) para gerenciar a implantação e escalabilidade.

### O que é CI/CD em microsserviços?
Integração Contínua e Entrega Contínua, automatizando testes e deploy para garantir atualizações rápidas e seguras.

### Como versionar APIs e garantir compatibilidade?
Usando versionamento semântico (ex: v1, v2) e garantindo retrocompatibilidade sempre que possível.

## 5. Escalabilidade e Resiliência
### Como escalar microsserviços?
- **Escalabilidade horizontal:** Adicionar mais instâncias de um serviço.
- **Escalabilidade vertical:** Aumentar recursos de uma instância.

### O que são padrões como Circuit Breaker, Retry e Bulkhead?
- **Circuit Breaker:** Interrompe chamadas a serviços falhos.
- **Retry:** Tenta novamente uma operação falha.
- **Bulkhead:** Isola recursos para evitar falhas em cascata.

### O que é Service Discovery e Load Balancing?
- **Service Discovery:** Permite que serviços encontrem outros serviços dinamicamente.
- **Load Balancing:** Distribui carga entre instâncias de um serviço.

## 6. Segurança
### Como garantir segurança entre microsserviços?
Usando autenticação (JWT, OAuth2) e autorização (RBAC) para controlar acesso.

### Como proteger APIs e comunicações internas?
Com TLS/SSL para criptografia e service mesh (ex: Istio) para gerenciar tráfego seguro.

## 7. Monitoramento e Observabilidade
### Como monitorar microsserviços?
Usando métricas, logs distribuídos (ELK Stack, Grafana Loki) e rastreamento (Jaeger, Zipkin).

### O que é Health Check e Distributed Tracing?
- **Health Check:** Verifica a saúde de um serviço.
- **Distributed Tracing:** Rastreia requisições através de múltiplos serviços.

## 8. Organização da Equipe
### Como estruturar times para trabalhar com microsserviços?
Times pequenos e cross-funcionais, cada um responsável por um ou mais serviços.

### Qual o papel de times cross-funcionais e ownership de serviços?
Garantir que cada time tenha autonomia e responsabilidade sobre seus serviços.

## 9. Migração de Monólito para Microsserviços
### Quando migrar?
Quando o monólito se torna difícil de manter, escalar ou evoluir.

### Quais estratégias usar (ex: Strangler Pattern)?
O Strangler Pattern substitui gradualmente partes do monólito por microsserviços.

## 10. Custos e Trade-offs
### Quais os custos operacionais de microsserviços?
Complexidade de gerenciamento, infraestrutura distribuída e sobrecarga de comunicação.

### Quando não usar microsserviços?
Quando a aplicação é pequena ou a complexidade não justifica os custos.

## 11. Casos de Uso e Exemplos
### Quem usa microsserviços na prática?
- **Netflix:** Para streaming escalável.
- **Amazon:** Para e-commerce e infraestrutura.
- **Uber:** Para gerenciamento de corridas em tempo real.

### Quais lições aprendidas com falhas em microsserviços?
- Monitoramento e observabilidade são essenciais.
- Comunicação clara entre times é crítica.
- Evitar decomposição excessiva.


