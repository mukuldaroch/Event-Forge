```txt
```

## EventForge — Microservices Event Platform

EventForge is a containerized microservices-based event management system.
It demonstrates secure service-to-service communication, domain isolation, and orchestrated workflows.

### Architecture Overview

- Microservices architecture
- Database per service
- Docker-based networking
- JWT-based authentication via Keycloak
- Orchestrator pattern for multi-service operations

### Services

| Service         | Responsibility                   | Database   |
| --------------- | -------------------------------- | ---------- |
| Event Service   | Event CRUD & publishing          | PostgreSQL |
| Ticket Service  | Ticket types, pricing, inventory | PostgreSQL |
| Booking Service | Booking of Tickets               | PostgreSQL |
| Orchestrator    | Multi-service coordination       | None       |
| API Gateway     | Entry point, rate limiting       | None       |

### Infrastructure

- All services run in Docker containers
- Communication via container names
- PostgreSQL per service
- Centralized auth via Keycloak

```txt

```

```txt

```

### Key Technical Highlights

- Spring Boot microservices
- OAuth2 Resource Server (JWT validation)
- Keycloak authentication
- Service-to-service JWT forwarding
- Independent DB per service
- Docker & Docker Compose setup
- Redis (caching)

### Design Principles

- Clear separation of concerns (Controller → Service → Repository)
- Domain-driven service boundaries
- Single responsibility per microservice
- RESTful API design conventions
- Database consistency via transactional boundaries

### Planned Extensions

- Payment Service
- Kafka-based Saga workflow
- Dead Letter Queue & retry policies
- Notification service
- Kubernetes deployment
- Centralized logging pipeline
