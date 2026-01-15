
# 🖊️ Section 5: Spring Boot 101

## How does Spring Boot work? — Architecture (Strong Recall Notes)

---

## Big picture first (mental model)

Spring Boot follows a **layered architecture**.
Each layer has **one clear responsibility** and talks only to nearby layers.

Main layers:

1. Presentation Layer
2. Service Layer
3. Data Access Layer

---

## Layered Architecture (at a glance)

```
User
 ↓
Presentation Layer (Controller)
 ↓
Service Layer (Business Logic)
 ↓
Data Access Layer (Repository)
 ↓
Database
```

Response flows back **upwards** in the same order.

---

## 1️⃣ Presentation Layer (Controller Layer)

What this layer is:

* Entry point of the application
* Talks directly to the user (browser / client)

What lives here:

* Controller classes (`@RestController`, `@Controller`)

What it does:

* Accepts HTTP requests
* Validates user input
* Calls service layer
* Sends response back to user

What it does NOT do:

* No business logic
* No database access

Think of it as:

> “Traffic police — receives requests and routes them correctly”

---

## 2️⃣ Service Layer (Business Logic Layer)

What this layer is:

* Heart of the application
* Contains business rules

What lives here:

* Service classes (`@Service`)

What it does:

* Implements business logic
* Processes data
* Makes decisions
* Coordinates between controller and repository

Communication:

* Called by controllers
* Calls repositories

Think of it as:

> “Brain of the application”

---

## 3️⃣ Data Access Layer (Repository Layer)

What this layer is:

* Database interaction layer

What lives here:

* Repository classes (`@Repository`)
* JPA repositories

What it does:

* Fetch data from DB
* Save data
* Update / delete data

Database type:

* Relational (MySQL, PostgreSQL)
* NoSQL (MongoDB)

What it does NOT do:

* No business logic
* No user interaction

Think of it as:

> “Messenger between app and database”

---

## Real-world Example: Library Management System

### Request Flow

```
User (Browser)
   ↓
Controller
   ↓
Service
   ↓
Repository
   ↓
Database
```

### Response Flow

```
Database
   ↑
Repository
   ↑
Service
   ↑
Controller
   ↑
User
```

---

## Step-by-step request journey (important for interviews)

1. User sends request from browser
2. Controller receives request
3. Controller forwards request to service
4. Service applies business logic
5. Service calls repository
6. Repository fetches data from database
7. Data returns back to service
8. Service processes response
9. Controller sends final response to user

---

## Why layered architecture is used

* Separation of concerns
* Easy to maintain
* Easy to test
* Easy to scale
* Clean code structure

Each layer has **one responsibility**.

---

## Clean responsibility mapping (memory hook)

```
Controller → Handles HTTP
Service    → Handles logic
Repository → Handles DB
```

---

## 🧠 One-Line Strong Recall

> **Spring Boot works using a layered architecture where controllers handle requests, services apply business logic, and repositories interact with the database.**
