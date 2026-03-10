```txt

```

## Booking Service — Microservice

The **Booking Service** is a transactional microservice responsible for managing the **booking lifecycle** of tickets. It handles:

- Creating bookings
- Reserving tickets
- Confirming bookings after payment
- Handling cancellation or failure

It acts as the **ownership transition layer** between Ticket Service and Payment Service.

### Booking Status Flow

> **CREATED → CONFIRMED → CANCELLED**
> **CREATED → FAILED**
> **CREATED → EXPIRED**

---

## API Endpoints

Bookings

| Method | Endpoint                         | Description                       |
| ------ | -------------------------------- | --------------------------------- |
| POST   | `/bookings`                      | Create a new booking              |
| GET    | `/bookings/{booking_id}`         | Retrieve booking details          |
| POST   | `/bookings/{booking_id}/confirm` | Confirm booking (payment success) |
| POST   | `/bookings/{booking_id}/fail`    | Mark booking as failed            |
| POST   | `/bookings/{booking_id}/cancel`  | Cancel booking                    |

```txt

```

```txt

```

User Bookings

| Method  | Endpoint                | Description                |
| ------- | ----------------------- | -------------------------- |
| **GET** | `/bookings?userId=uuid` | Get all bookings of a user |

---

## Booking-Service Project Structure

```bash
src/
 ├── config
 ├── controllers
 ├── domain
 │   ├── entities
 │   └── enums
 ├── dto
 │   └── booking
 │       ├── request
 │       └── response
 ├── exceptions
 ├── mappers
 ├── repositories
 └── services
```

## Future Plans

- Ticket Reservation Timeout Handling
- Idempotent Booking Creation
- Booking Status History Tracking
- Integration with Payment Service (Async Confirmation)
- Integration with Ticket Service (Inventory Reservation & Release)
