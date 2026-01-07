## 1️⃣ Why Do We Need Different Types of API Requests?

In web applications:

* Sometimes we **read** data
* Sometimes we **create** data
* Sometimes we **update** data
* Sometimes we **delete** data

📌 Using one request type for everything would be confusing and unsafe.

That’s why APIs use **different request types**, also called **HTTP methods**.

---

## 2️⃣ What Are HTTP Methods?

### 🔹 Simple Definition

HTTP methods are **actions** that tell the server:

> “What do you want to do with this resource?”

---

### CRUD Mapping (VERY IMPORTANT)

| Operation | Meaning      | HTTP Method |
| --------- | ------------ | ----------- |
| Create    | Add new data | POST        |
| Read      | Get data     | GET         |
| Update    | Change data  | PUT         |
| Delete    | Remove data  | DELETE      |

📌 This mapping is **fundamental** in REST APIs.

---

## 3️⃣ GET Request

### 🔹 What is GET?

A **GET request** is used to **retrieve (read) data** from the server.

📌 GET = Read only
📌 GET should **not** change data

---

### 🔹 Example

```
GET /products
```

Meaning:

> “Give me all products”

---

### 🔹 GET Characteristics

* Used only to read data
* No data modification
* Safe request
* Can be cached
* Often used in browser

---

### 🔹 GET Diagram

```
Client
  |
  | GET /products
  v
Server
  |
  | Product List
  v
Client
```

---

## 4️⃣ POST Request

### 🔹 What is POST?

A **POST request** is used to **create new resources** on the server.

📌 POST = Create data

---

### 🔹 Example

```
POST /products
```

Request body:

```json
{
  "name": "Laptop",
  "price": 50000
}
```

Meaning:

> “Create a new product”

---

### 🔹 POST Characteristics

* Sends data to server
* Creates new resource
* Data sent in request body
* Not cached
* Used for forms, login, registration

---

### 🔹 POST Diagram

```
Client
  |
  | POST /products
  | { product data }
  v
Server
  |
  | Product Created
  v
Client
```

---

## 5️⃣ PUT Request

### 🔹 What is PUT?

A **PUT request** is used to **update existing resources** on the server.

📌 PUT = Update data

---

### 🔹 Example

```
PUT /products/1
```

Request body:

```json
{
  "name": "Gaming Laptop",
  "price": 70000
}
```

Meaning:

> “Update product with ID 1”

---

### 🔹 PUT Characteristics

* Updates existing data
* Usually requires resource ID
* Replaces existing data
* Sends full updated data

---

### 🔹 PUT Diagram

```
Client
  |
  | PUT /products/1
  | { updated data }
  v
Server
  |
  | Product Updated
  v
Client
```

---

## 6️⃣ DELETE Request

### 🔹 What is DELETE?

A **DELETE request** is used to **remove a resource** from the server.

📌 DELETE = Remove data

---

### 🔹 Example

```
DELETE /products/1
```

Meaning:

> “Delete product with ID 1”

---

### 🔹 DELETE Characteristics

* Removes data permanently
* Requires resource ID
* No request body usually
* Dangerous if misused

---

### 🔹 DELETE Diagram

```
Client
  |
  | DELETE /products/1
  v
Server
  |
  | Product Deleted
  v
Client
```

---

## 7️⃣ One Resource – All Operations (Big Picture)

```
/products
   |
   ├─ GET    → Get all products
   ├─ POST   → Create new product
   |
/products/{id}
   |
   ├─ GET    → Get one product
   ├─ PUT    → Update product
   ├─ DELETE → Delete product
```

📌 Same URL, different **methods**, different actions.

---

## 8️⃣ Why REST APIs Follow This Pattern

* Clear meaning
* Easy to understand
* Industry standard
* Scales well
* Secure by design

---

## 9️⃣ How This Connects to Spring Boot (Preview)

Later in Spring Boot:

* `@GetMapping` → GET
* `@PostMapping` → POST
* `@PutMapping` → PUT
* `@DeleteMapping` → DELETE

📌 Each API method maps to one HTTP method.

---

## 🧠 VIDEO 4 – DEEP KEY TAKEAWAYS (HAND NOTES READY)

✍️ Write these carefully in your notebook:

* APIs use HTTP methods to perform actions
* HTTP methods define what operation to perform
* GET request is used to read data from server
* GET should not modify data
* POST request is used to create new resources
* POST sends data in request body
* PUT request is used to update existing resources
* PUT usually requires resource ID
* DELETE request removes a resource from server
* CRUD operations map to HTTP methods
* Same URL can behave differently based on method
* REST APIs follow this standard strictly

---

## 🧩 One-Line Recall (Interview Friendly)

> “REST APIs use HTTP methods like GET, POST, PUT, and DELETE to perform CRUD operations on resources.”

---

**Thank you**

---

### Next?

Say:
👉 **“What is REST API and its Architecture?”**
