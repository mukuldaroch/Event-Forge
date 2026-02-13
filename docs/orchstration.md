# Orchestrator Service

A service whose only job is to coordinate multiple domain services to fulfill a single business operation.
Creating an event with ticket types is **one business action** — but **two microservices** must act.
That’s what this service does.

This service is the **command and coordination layer** between:

- **Event Service**
- **Ticket Service**

The orchestrator exposes **one clean API** to the outside world and internally calls to multiple microservices, handling:

- Event creation
- Ticket type creation
- Error handling and rollback logic

---

## API Endpoints

| Method | Endpoint                | What it does                                        | Who actually handles it                |
| ------ | ----------------------- | --------------------------------------------------- | -------------------------------------- |
| POST   | `/api/events`           | Creates an event **and** its ticket types in one go | Orchestrator → Event + Ticket services |
| GET    | `/api/events/{eventId}` | Fetches event details                               | Event Service (via Orchestrator)       |
| PATCH  | `/api/events/{eventId}` | Updates event metadata                              | Event Service (via Orchestrator)       |
| DELETE | `/api/events/{eventId}` | Deletes the event and all related ticket types      | Orchestrator → Event + Ticket services |

---

# 🏗 High Level Flow

When a client calls:

```
POST /api/events
```

The orchestrator performs:

```
Client
  │
  ▼
Orchestrator
  │
  ├──▶ Event Service (create event)
  │          │
  │          └── returns eventId
  │
  └──▶ Ticket Service (create ticket types using eventId)
```

---

# Project Structure

```
src
└── main.java.com.daroch.orchestrator
    │   ├── config            ( WebClient )
    │   ├── controller
    │   ├── dto
    │   │   ├── api           ( Public API contracts )
    │   │   │   ├── request
    │   │   │   └── response
    │   │   │
    │   │   ├── eventservice  ( Contracts used when calling Event Service )
    │   │   │
    │   │   └── ticketservice ( Contracts used when calling Ticket Service )
    │   ├── exception
    │   ├── mapper      ( Converts API DTOs → service DTOs)
    │   └── service
    │       ├── client  ( Interfaces for external service calls )
    │       └── impl    ( Orchestration logic )
    │
    └── resources
```

---

## Authentication

All endpoints require a **JWT from Keycloak**.

The orchestrator **forwards the same JWT** to:

- Event Service
- Ticket Service

## Future Plans

- Distributed Consistency & Rollback Strategy
- Idempotency Support
- Partial Failure State Tracking
- logging
