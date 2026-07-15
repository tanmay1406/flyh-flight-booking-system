# ✈️ FlyH - Flight Booking System

A scalable airline management and flight booking platform built using a Microservices Architecture. The system is designed to handle flight management, secure bookings, user authentication, asynchronous notifications, and concurrent booking requests while maintaining reliability and scalability.

---

## Architecture Overview

The project consists of four independent microservices:

| Service              | Description                                                                            |
| -------------------- | -------------------------------------------------------------------------------------- |
| Flight Service       | Handles flight, airport, city, airplane and seat management APIs                       |
| Booking Service      | Manages flight bookings, transactions and seat reservations                            |
| API Gateway          | Provides authentication, authorization and acts as the entry point for client requests |
| Notification Service | Sends email notifications asynchronously after successful bookings                     |

### High Level Design

```
                        Client
                           |
                           |
                     API Gateway
                           |
         ---------------------------------------
         |                 |                   |
         |                 |                   |
   Flight Service    Booking Service      Authentication
         |                 |                  (JWT)
         |                 |
      MySQL            MySQL Database
                           |
                      RabbitMQ Queue
                           |
                    Notification Service
                           |
                     Email Notifications
```

---

## Tech Stack

* Node.js
* Express.js
* MySQL
* Sequelize ORM
* JWT Authentication
* RabbitMQ
* Nodemailer
* Winston Logger
* Sequelize CLI
* Cron Jobs
* REST APIs

---

## Features

### Flight Management

* Flight CRUD operations
* Airport management
* City management
* Airplane management
* Seat management
* Flight searching and filtering
* Dynamic seat availability handling

### Secure Authentication

* User registration and login
* JWT based authentication
* Role Based Authorization
* Protected API endpoints
* Password hashing using bcrypt

### Booking Management

* Flight ticket booking
* Database transactions for consistency
* Seat reservation handling
* Concurrency management
* Payment workflow support
* Automatic booking status updates

### Notification Service

* Email notifications
* RabbitMQ based asynchronous communication
* Booking confirmations
* Ticket generation support

---

## System Design Considerations

The project has been designed keeping the following requirements in mind:

* High read traffic for flight searches.
* Reliable booking transactions.
* Concurrent booking requests for the same seat.
* Prevention of overbooking.
* Scalable microservices architecture.
* Independent deployment of services.
* Asynchronous notification handling.

### Concurrency Challenges

The system addresses problems such as:

* Multiple users booking the same seat simultaneously.
* Failed payment transactions.
* Client failures after successful payments.
* Seat locking during booking operations.

Database transactions are used wherever consistency is critical to ensure atomic operations.

---

## Folder Structure

```
FlyH
│
├── API_GATEWAY
│   └── Authentication & Authorization
│
├── Flights-Service
│   └── Flight Management APIs
│
├── Booking-Service
│   └── Booking Management APIs
│
├── Notification-Service
│   └── Email Notification APIs
│
└── README.md
```

### Flight Service

Responsible for:

```
Flights
Airplanes
Airports
Cities
Seats
Flight Search APIs
```

### Booking Service

Responsible for:

```
Booking Creation
Booking Updates
Transaction Management
Seat Reservation
Concurrency Handling
```

### API Gateway

Responsible for:

```
Authentication
Authorization
JWT Validation
Rate Limiting
User Management
API Routing
```

### Notification Service

Responsible for:

```
Email Notifications
RabbitMQ Consumers
Ticket Management
Booking Confirmations
```

---

## Installation

### Clone the Repository

```bash
git clone <repository-url>

cd flyh-flight-booking-system
```

### Install Dependencies

For every microservice:

```bash
npm install
```

or

```bash
cd API_GATEWAY
npm install

cd ../Flights-Service
npm install

cd ../Booking-Service
npm install

cd ../Notification-Service
npm install
```

---

## Environment Variables

Create a `.env` file inside every service directory using the provided `example.env` file.

Example:

```bash
PORT=
DB_HOST=
DB_NAME=
DB_USERNAME=
DB_PASSWORD=
JWT_SECRET=
EMAIL=
EMAIL_PASSWORD=
```

---

## Running the Services

### Development Mode

```bash
npm run dev
```

### Production Mode

```bash
npm start
```

Run every microservice independently.

---

## Database Setup

Run migrations:

```bash
npx sequelize-cli db:migrate
```

Run seeders if required:

```bash
npx sequelize-cli db:seed:all
```

Rollback migrations:

```bash
npx sequelize-cli db:migrate:undo
```

---

## Microservice Communication

```
                   Booking Service
                           |
                    Creates Booking
                           |
                    Publishes Event
                           |
                       RabbitMQ
                           |
                    Notification Service
                           |
                     Sends Email
                           |
                          User
```

Using asynchronous communication allows:

* Loose coupling between services.
* Improved scalability.
* Better fault tolerance.
* Independent deployments.

---

## Reliability and Scalability

The system has been designed to support:

* Horizontal scaling.
* High availability.
* Fault isolation.
* Independent service deployment.
* Reliable transaction handling.
* Concurrent booking management.
* Asynchronous event processing.

---

## Future Improvements

* Docker support
* Kubernetes deployment
* Payment gateway integration
* Redis caching
* CI/CD pipelines
* API documentation using Swagger
* Circuit breakers for fault tolerance
* Distributed tracing and monitoring

---

## Learning Outcomes

This project demonstrates practical implementation of:

* Microservices Architecture
* Database Transactions
* Concurrency Handling
* JWT Authentication & Authorization
* RabbitMQ Messaging
* REST API Design
* Sequelize ORM
* Scalable Backend Design
* Event Driven Systems
* Asynchronous Communication Patterns

---

## Contributors

Built as a scalable backend system for airline management and flight booking using modern backend engineering principles.
