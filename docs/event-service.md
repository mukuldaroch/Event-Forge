```txt

```

## Event Service — Microservice

The **Event Service** is a core **microservice** within the EventForge ecosystem responsible for managing the **event lifecycle**. It provides backend APIs for **creating, updating, publishing, and retrieving events**, and acts as the source of truth for event-related data.

### Event Status Flow:

> **DRAFT → PUBLISHED → CLOSED PUBLISHED → CANCELLED**

### Internal Architecture

> **Controller → Service → Repository → Database**

---

## API Endpoints

events

| Method     | Endpoint             | Description            |
| ---------- | -------------------- | ---------------------- |
| **POST**   | `/events`            | Create a new event     |
| **GET**    | `/events/{event_id}` | Retrieve event details |
| **PATCH**  | `/events/{event_id}` | Update event details   |
| **DELETE** | `/events/{event_id}` | Delete an event        |

Public Events

| Method  | Endpoint                       | Description                 |
| ------- | ------------------------------ | --------------------------- |
| **GET** | `/events/published`            | List all published events   |
| **GET** | `/events/published/{event_id}` | Get published event details |

```txt

```

## Event-Service Project Structure

```bash
├── main
│   ├── java.com.daroch.event
│   │   ├── config
│   │   ├── controllers
│   │   ├── domain
│   │   │   ├── entities
│   │   │   └── enums
│   │   ├── dto
│   │   │   ├── commands
│   │   │   ├── concrete
│   │   │   ├── request
│   │   │   └── response
│   │   ├── exceptions
│   │   ├── mappers
│   │   ├── repositories
│   │   └── services
│   │
│   └── resources
└── test.java.com.daroch.event
     ├── controllers
     ├── repositories
     └── services
```
