# EventForge — Microservices-Based Event Platform

**EventForge** is a **microservices-based event management system** designed to handle the complete lifecycle of events—from creation and ticketing to payments, monitoring, and validation.

The platform is built with a **distributed architecture**, where each core domain is isolated into its own service, enabling scalability, fault isolation, and independent development.

The system supports three primary roles:

- **Organizers** – create and manage events, configure tickets, track sales
- **Attendees** – browse events, purchase tickets, and access event passes
- **Staff** – validate tickets and manage on-ground event operations
  ![ Roles ](docs/assets/events/roles.jpg)

---

## Microservices Architecture

![ EventForge Architecture Diagram ](docs/assets/events/event-forge.jpg)

![ Database Architecture Diagram ](docs/assets/events/ERD-Diagram.jpg)

![ Event-Service Architecture Diagram ](docs/assets/events/event-service.jpg)
![ Ticket-Service Architecture Diagram ](docs/assets/events/ticket-service.jpg)
![ Orchestration-Service Architecture Diagram ](docs/assets/events/orchstration-service.jpg)

![ Booking-Service Architecture Diagram ](docs/assets/events/booking-service.jpg)
![ Payment-Service Architecture Diagram ](docs/assets/events/payment-service.jpg)

## [ EventForge Full Architecture Design link](https://miro.com/app/board/uXjVGVq5l3U=/?moveToWidget=3458764653985736600&cot=14)

---

## Services in this repository

The platform is composed of multiple independent services, including:

| Service             | What it owns           | What it does                                    |
| ------------------- | ---------------------- | ----------------------------------------------- |
| **Event Service**   | Events                 | Creates, updates, publishes and exposes events  |
| **Ticket Service**  | Ticket types & tickets | Manages pricing, inventory, and ticket issuance |
| **Booking Service** | Booking of a Event     | Booking of ticket types of a event              |
| **Payment Service** | Payments               | Payment for a Bookings                          |
| **Orchestrator**    | Nothing                | Coordinates multi-service operations            |
| **Gateway**         | Nothing                | Coordinates api requests , rate limiting        |

> **Github links for each microservice main branch:**
>
> - [Event Service](https://github.com/mukuldaroch/event-service)
> - [Ticket Service](https://github.com/mukuldaroch/ticket-service)
> - [Orchestration Service](https://github.com/mukuldaroch/orchestration-service)
> - [Gateway Service ](https://github.com/mukuldaroch/gateway-service)
> - [Gateway Service ](https://github.com/mukuldaroch/payment-service)

---

## Tech Stack

- **Backend:** Spring Boot (Java 17)
- **Build Tool:** Gradle
- **Database:** PostgreSQL
- **Containerization:** Docker & Docker Compose
- **Auth:** Keycloak JWT-based Authentication
- **Deployment:** Dockerized microservice setup

---

## 🐳 Running the whole platform

High-level startup order:

1. Docker network
2. PostgreSQL containers
3. Keycloak
4. Event Service
5. Ticket Service
6. Orchestrator

## Each service README explains how to start each microservice.

They all join the same Docker network so they can talk via container names.

---

| Service                  | Container Name         | Internal Port | Exposed Port |
| ------------------------ | ---------------------- | ------------- | ------------ |
| **Keycloak**             | `keycloak`             | 8080          | 8080         |
| **Redis**                | `redis`                | 6379          | 6379         |
| **event-service**        | `event-service`        | 8080          | 8083         |
| **orchestrator-service** | `orchestrator-service` | 8080          | 8082         |
| **ticket-service**       | `ticket-service`       | 8080          | 8084         |
| **booking-service**      | `booking-service`      | 8080          | 8085         |
| **payment-service**      | `booking-service`      | 8080          | 8086         |
| **event-database**       | `event-database`       | 5432          | 5432         |
| **ticket-database**      | `ticket-database`      | 5434          | 5434         |
| **booking-database**     | `booking-database`     | 5432          | 5435         |
| **payment-database**     | `payment-database`     | 5432          | 5436         |

---

## 🔐 Security Model

Users authenticate once and receive a **JWT**.

Each service validates the token independently.

---

## 📦 Repository Layout

This repository uses a **multi-repo microservice model** (each service can be cloned and deployed independently), but architecturally it behaves as one system.

```
eventforge/
├── event-service/
├── ticket-service/
├── orchestrator-service/
├── gateway-service/
├── payment-service/
└── docs/
    └── architecture diagrams
```

Each service has its own:

- Dockerfile
- Database
- README
- Deployment model

---

## Engineering Principles Behind This

EventForge uses:

- OAuth2 Resource Server (JWT)
- Isolated databases
- Docker networking
- Service-to-service authentication
- Event Driven architecture

---

## Future Plans

Planned services:

- Notification Service
- Centralized logging

The architecture already supports them.

---

## 👨‍💻 Author

- [@Mukul Daroch](https://github.com/mukuldaroch)
