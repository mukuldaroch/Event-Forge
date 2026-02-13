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

| Service        | Responsibility                   | Database   |
| -------------- | -------------------------------- | ---------- |
| Event Service  | Event CRUD & publishing          | PostgreSQL |
| Ticket Service | Ticket types, pricing, inventory | PostgreSQL |
| Orchestrator   | Multi-service coordination       | None       |
| API Gateway    | Entry point, rate limiting       | None       |

### Key Technical Highlights

- Spring Boot microservices
- OAuth2 Resource Server (JWT validation)
- Keycloak authentication
- Service-to-service JWT forwarding
- Independent DB per service
- Docker & Docker Compose setup
- Redis (caching)

### Orchestration Example

Creating an event with tickets:

1. Orchestrator receives request
2. Calls Event Service
3. Calls Ticket Service
4. Handles failure scenarios
5. Returns aggregated response

Business action → multiple service calls → coordinated centrally.

### Infrastructure

- All services run in Docker containers
- Communication via container names
- PostgreSQL per service
- Centralized auth via Keycloak

### Planned Extensions

- Payment Service
- Kafka-based Saga workflow
- Dead Letter Queue & retry policies
- Notification service
- Kubernetes deployment
- Centralized logging pipeline
