# ⚙️ Reactive Spring Boot Microservices with OAuth, Docker, and Kubernetes

## 🎯 Purpose

This project was built to develop hands-on understanding of **distributed system behaviour from an engineering and testability perspective**.

The goal was not just to build microservices, but to explore:
- how services interact under normal and failure conditions  
- how asynchronous messaging affects system behaviour  
- how security boundaries (OAuth 2.0 / OIDC) influence system design  
- how such systems can be **tested deterministically across layers**

---

## 🧠 System Overview

The system models a typical microservices architecture:

- API Gateway as the entry point  
- Multiple backend services (product, review, recommendation)  
- Service discovery and configuration management  
- Asynchronous communication via Kafka and RabbitMQ  
- Secure service-to-service interaction via OAuth 2.0 / OIDC  

The focus is on **flow-based behaviour**, where requests propagate across services and result in durable system state.

![System Diagram](system-diagram.png)

---

## ⚠️ System Behaviour & Failure Scenarios

This project explores realistic distributed system concerns:

- **Transient failures** (timeouts, unavailable services)  
- **Retry behaviour and recovery patterns**  
- **Eventual consistency across asynchronous flows**  
- **Message delivery and ordering considerations**  
- **Security failures (invalid/expired tokens)**  

These scenarios were used to understand:
- how failures propagate across service boundaries  
- how systems recover and stabilise  
- how to design tests that remain reliable despite non-determinism  

---

## 🚀 Tech Stack

- **Spring Boot (WebFlux)** — Reactive microservices  
- **OAuth 2.0 + OIDC** — Authentication and token validation  
- **Docker & Docker Compose** — Containerised execution  
- **Kafka & RabbitMQ** — Event-driven communication  
- **Gradle Multi-Project** — Modular build structure  

---

## 📁 Project Structure

| Folder | Description |
|--------|-------------|
| `api/` | API gateway and routing |
| `microservices/` | Core business services |
| `spring-cloud/` | Config server, discovery, gateway |
| `keystore/` | TLS and OAuth/OIDC setup |
| `util/` | OpenAPI specs and shared utilities |

---

## 🔐 Security Architecture

- OAuth 2.0 / OIDC integration via Spring Security  
- Token validation at service boundaries  
- Role-based access control using scopes and claims  
- HTTPS enforced via keystore configuration  

---

## 🧪 Testing Strategy

Testing is structured across multiple layers to reflect real-world system validation:

### Unit Tests
- Validate core business logic in isolation  

### Component Tests
- Validate service-level behaviour with controlled dependencies  
- Focus on API contracts and internal logic  

### Integration Tests
- Validate end-to-end flows via the API gateway  
- Ensure correct interaction across services and messaging layers  

### Key Focus Areas
- Reactive flow validation (WebFlux)  
- OAuth token validation and security boundaries  
- Service interaction through Kafka and RabbitMQ  
- Deterministic testing of asynchronous behaviour where possible  

Tests are executed during build and CI workflows to provide fast and reliable feedback.

---

## 🧪 Running Tests

```bash
./gradlew test
```
For a specific module:

```bash
./gradlew :<module-name>:test
```

---

## 🧪 Local System Execution & Sanity Testing

A test harness is provided to run the full system locally using Docker.

### Prerequisites
- Docker installed and running
- Git
- Bash (Linux/macOS or WSL)

### Clone Repository

```bash
git clone https://github.com/kiduknott/akt-reactive-springboot-cloud-kubernetes-microservices-with-oauth.git
cd akt-reactive-springboot-cloud-kubernetes-microservices-with-oauth
```
### Start System and Run Sanity Tests

```bash
./test-all-microservices-on-docker-via-product-composite-02.bash start
```

This will:
- Build and start all services
- Route traffic through the API gateway
- Initialise Kafka and RabbitMQ
- Execute basic system-level validation

### Stop System

```bash
./test-all-microservices-on-docker-via-product-composite-02.bash stop
```

---

## 🔍 How to Evaluate This Project

To assess this project:
1. Run the system using Docker
2. Execute the test script
3. Observe:
- request flow through the API gateway
- service interactions
- messaging behaviour (Kafka/RabbitMQ)
- system behaviour during startup/shutdown

Focus on how the system behaves under interaction, not just individual endpoints.

---
