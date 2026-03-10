```txt

```

## Ticket Service — EventManagment Microservice

The **Ticket Service** is a dedicated **microservice** within the Event ecosystem that handles **all ticket-related operations**. It provides backend API for **creating, managing Ticket types** for events.

### Ticket Status Flow

> **PURCHASED -> CANCELLED -> EXPIRED**

---

## API Endpoints

| Method     | Endpoint                                    | Description                        |
| ---------- | ------------------------------------------- | ---------------------------------- |
| **GET**    | `/ticket-types?{event-id}`                  | List all ticket types for an event |
| **GET**    | `/ticket-types/{ticket_type_id}`            | Retrieve ticket type details       |
| **PATCH**  | `/ticket-types/{ticket-type-id}?{event-id}` | Update ticket type                 |
| **DELETE** | `/ticket-types/{ticket_type_id}`            | Delete ticket type                 |

Tickets

| Method     | Endpoint              | Description                  |
| ---------- | --------------------- | ---------------------------- |
| **POST**   | `/ticket`             | Create tickets for a event   |
| **GET**    | `/ticket`             | List all tickets for a event |
| **GET**    | `/ticket/{ticket_id}` | Retrieve details of a ticket |
| **PATCH**  | `/ticket{ticket_id}`  | Update ticket info           |
| **DELETE** | `/ticket{ticket_id}`  | Delete a ticket of a event   |

```txt

```

## Ticket-Service Project Structure

```bash
main.java.com.daroch.ticket
 ├── config
 ├── controllers
 ├── domain
 │   ├── entities
 │   └── enums
 ├── dto
 │   ├── ticket
 │   ├── commands
 │   └── tickettype
 ├── exceptions
 ├── mappers
 ├── repositories
 └── services
     └── impl
         ├── ticket
         └── tickettype

```

## Future Plans

- QR code generation & validation for tickets
- Email confirmation for purchased tickets
- Real-time analytics for ticket sales
- Concurrency Protection
