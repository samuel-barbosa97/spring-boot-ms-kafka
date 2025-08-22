# Spring Boot Microservices com Apache Kafka  

Este projeto demonstra a implementação de uma **arquitetura de microservices** utilizando **Spring Boot**, **Apache Kafka** e **Docker**, com foco em comunicação assíncrona, escalabilidade e boas práticas de isolamento de serviços.  

## 📌 Arquitetura  

A solução foi construída baseada em **event-driven architecture (EDA)**, onde os microservices se comunicam de forma desacoplada através de tópicos Kafka.  

![Arquitetura Microservices](https://github.com/user-attachments/assets/e97cea5a-1ff8-4132-b956-b33f9bec00b3)

### Fluxo de Processos (numerado na imagem)  
1. O usuário (via Mobile ou Web) cria um pedido.  
2. O microserviço **Pedidos** envia a transação ao **Banco**.  
3. O **Banco** retorna o status do pagamento.  
4. O microserviço **Pedidos** publica o evento de pagamento no Kafka.  
5. O microserviço **Faturamento** recebe o pedido pago.  
6. O **Faturamento** publica o evento de faturamento no Kafka.  
7. O microserviço **Logística** recebe a notificação de faturamento e cadastra o rastreamento.  
8. A **Logística** publica o evento de envio do pedido no Kafka.  

Cada serviço possui seu **banco de dados independente**, reforçando o princípio de isolamento.  

---

## 🛠️ Tecnologias Utilizadas  

- **Java 21**  
- **Spring Boot** (Web, Data, Kafka, Validation)  
- **Apache Kafka** (event streaming)  
- **Docker & Docker Compose** (orquestração dos serviços externos)  
- **PostgreSQL** (bancos independentes para cada microservice)  
- **MinIO** (armazenamento de objetos, compatível com S3)  
- **Jasper Reports** (relatórios dinâmicos)  

---

## 🚀 Funcionalidades  

- Microservices independentes para **Produtos, Clientes, Pedidos, Faturamento e Logística**  
- Comunicação **assíncrona via Kafka**  
- Persistência de dados em bancos separados por contexto  
- Integração com **Banco (simulação de instituição financeira)** para pagamentos  
- Geração de relatórios com JasperReports  
- Integração com **MinIO** para armazenamento de arquivos  
- Exposição de APIs REST para manutenção de clientes, produtos e pedidos  

---

## 📂 Estrutura do Projeto  

```bash
spring-boot-ms-kafka/
│── pedidos-service/
│── clientes-service/
│── produtos-service/
│── faturamento-service/
│── logistica-service/
│── common-library/         # classes compartilhadas
│── docker-compose.yml      # Kafka, Zookeeper, MinIO, PostgreSQL
│── docs/arquitetura.jpg    # Diagrama da arquitetura
└── README.md
````

---

## ▶️ Como Executar

### 1. Subir os serviços externos (Kafka, Zookeeper, MinIO, PostgreSQL)

```bash
docker-compose up -d
```

### 2. Rodar os microservices

Em cada módulo:

```bash
./mvnw spring-boot:run
```

### 3. Acessar os serviços

* **Produtos API** → `http://localhost:8081`
* **Clientes API** → `http://localhost:8082`
* **Pedidos API** → `http://localhost:8083`
* **Faturamento API** → `http://localhost:8084`
* **Logística API** → `http://localhost:8085`
* **MinIO Console** → `http://localhost:9000`
* **Kafka UI (se configurado)** → `http://localhost:8080`

---

## 📊 Diferenciais do Projeto

* **Arquitetura orientada a eventos** (EDA)
* **Escalabilidade horizontal** com microservices independentes
* **Isolamento de dados** por banco
* **Comunicação resiliente** com Kafka
* **Integração com serviços externos** (Webhooks, MinIO, Banco simulado)

---

## 📖 Próximos Passos

* Implementar **observabilidade** (Grafana, Prometheus, ELK Stack)
* Adicionar **testes de integração** com Kafka Testcontainers
* Publicar os serviços em **Kubernetes**

---

## 👨‍💻 Autor

**Samuel Barbosa**
[GitHub](https://github.com/samuel-barbosa97) | [LinkedIn](https://www.linkedin.com/in/barbosa-samuel97/)
