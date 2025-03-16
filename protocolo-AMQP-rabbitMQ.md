# README - AMQP e RabbitMQ

## 🔹 Introdução
Este documento aborda conceitos fundamentais sobre o protocolo **AMQP (Advanced Message Queuing Protocol)** e seu uso no **RabbitMQ**.

## 🔹 O que é o AMQP?
O **AMQP** é um protocolo aberto de mensagens usado para comunicação assíncrona entre sistemas distribuídos. Ele define como as mensagens são enviadas, roteadas e entregues.

## 🔹 Componentes principais do AMQP no RabbitMQ
1. **Producer (Produtor)** → Envia mensagens para uma **exchange**.
2. **Exchange** → Encaminha mensagens para **queues** com base em regras de roteamento.
3. **Queue (Fila)** → Armazena mensagens até que um **consumer** as processe.
4. **Consumer (Consumidor)** → Recebe e processa mensagens da fila.
5. **Binding** → Liga uma **exchange** a uma **queue**, podendo usar uma **routing key**.
6. **Routing Key** → Define regras de roteamento entre **exchange** e **queue**.

## 🔹 Tipos de Exchanges
- **Direct Exchange** → Usa **routing keys** para entregar mensagens a filas específicas.
- **Fanout Exchange** → Ignora **routing keys** e entrega mensagens a todas as filas vinculadas.
- **Topic Exchange** → Usa **routing keys** com padrões flexíveis (exemplo: `logs.info`, `logs.*`).
- **Headers Exchange** → Roteia mensagens baseado em cabeçalhos personalizados.

## 🔹 Binding e Routing Key
- O **binding** pode usar **routing keys**, mas nem sempre é necessário.
- No **Direct Exchange** e **Topic Exchange**, o **binding sempre usa routing keys**.
- No **Fanout Exchange**, a **routing key é ignorada**.

## 🔹 Benefícios do AMQP no RabbitMQ
✔️ Padroniza a comunicação entre sistemas distribuídos.
✔️ Permite desacoplamento entre produtor e consumidor.
✔️ Suporta confirmação de entrega e persistência de mensagens.
✔️ Funciona com diversas linguagens de programação.

## 🔹 Conclusão
O AMQP é um protocolo poderoso para sistemas assíncronos, e o RabbitMQ é uma implementação popular dele. Compreender os conceitos de **exchange, queues, bindings e routing keys** é essencial para utilizar eficientemente o RabbitMQ.

