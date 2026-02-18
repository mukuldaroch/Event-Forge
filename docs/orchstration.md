## Orchestrator Service

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

Booking APIs

| Method | Endpoint                           | Description                         | Flow                             |
| ------ | ---------------------------------- | ----------------------------------- | -------------------------------- |
| POST   | `/api/bookings`                    | Create booking and initiate payment | Orchestrator → Booking → Payment |
| GET    | `/api/bookings/{bookingId}`        | Fetch booking details               | Orchestrator → Booking           |
| POST   | `/api/bookings/{bookingId}/cancel` | Cancel booking                      | Orchestrator → Booking           |

---

## 🏗 High Level Flow

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

## Booking + Payment Flow (Critical Path)

When client creates booking:

```
Client
  │
  ▼
Orchestrator
  │
  ├──▶ Booking Service
  │        POST /bookings
  │        returns bookingId
  │
  ├──▶ Payment Service
  │        POST /payments
  │        returns SUCCESS / FAILED
  │
  ├──▶ if SUCCESS
  │        Booking Service
  │        POST /bookings/{id}/confirm
  │        POST /ticket/
  │
  └──▶ if FAILED
           Booking Service
           POST /bookings/{id}/fail
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
- Booking Service
- Payment Service

## Future Plans

- Distributed Consistency & Rollback Strategy
- Idempotency Support
- Partial Failure State Tracking
- logging
