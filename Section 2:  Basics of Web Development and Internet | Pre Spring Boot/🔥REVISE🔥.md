# 📘 SECTION 1 – BASICS OF WEB DEVELOPMENT & INTERNET

---

## 🎥 VIDEO 1 – How Does the Web Work?

### ✍️ My Self-Explanation (What I Learned)

In this video, I learned **how the web actually works behind the scenes**.

The **Internet** is a global network of computers connected to each other.
The **World Wide Web (WWW)** is just a way to access information using the internet.

When I type a website name like `www.google.com`:

* My browser does **not understand names**
* It converts the domain name into an **IP address**
* Then it sends a request to the server using that IP

The server receives my request and sends back a response (HTML, JSON, etc.).

So basically, **web = request + response**.

---

### 🖼️ Diagram – How Web Works

```
Browser
   |
   | Request (domain name)
   v
DNS → IP Address
   |
   v
Server
   |
   | Response (data)
   v
Browser
```

---

### 🧠 Key Memory Points

* Internet = network of computers
* Web = way to access information
* Domain name → IP address
* Browser sends request
* Server sends response

---

## 🎥 VIDEO 2 – What is Client & Server?

### ✍️ My Self-Explanation

In this video, I understood **who talks to whom on the web**.

A **Client** is:

* Something that requests data
* Usually a browser, mobile app, or software
* Shows UI and receives data

A **Server** is:

* Always running
* Handles multiple clients
* Stores logic and data
* Sends responses

Client **asks**, Server **serves**.

---

### 🖼️ Diagram – Client Server Interaction

```
Client (Browser / App)
        |
        | Request
        v
      Server
        |
        | Response
        v
Client
```

---

### 🧠 Key Memory Points

* Client requests data
* Server provides data
* Client = UI
* Server = logic + data
* Many clients → one server

---

## 🎥 VIDEO 3 – What Are APIs?

### ✍️ My Self-Explanation

This video taught me **how two software systems talk**.

API = **Application Programming Interface**

An API acts like a **middleman** between:

* Client (browser / app)
* Server (backend / database)

The restaurant example helped a lot:

* Customer → Application
* Waiter → API
* Kitchen → Backend
* Food → Response

APIs:

* Automate communication
* Reduce manual work
* Make systems reusable

APIs can be:

* Public
* Private
* Partner

---

### 🖼️ Diagram – API Flow

```
Client
   |
   | Request
   v
API (Server)
   |
   | Backend logic + DB
   v
Response
```

---

### 🧠 Key Memory Points

* API is a bridge
* Client never talks directly to database
* API validates request
* API returns response
* APIs automate systems

---

## 🎥 VIDEO 4 – Types of API Requests

### ✍️ My Self-Explanation

Here I learned **how clients perform actions on servers**.

REST APIs use **HTTP methods**:

* GET → Read data
* POST → Create data
* PUT → Update data
* DELETE → Remove data

Each method has **one clear purpose**.

---

### 🖼️ Diagram – CRUD Mapping

```
GET     → READ
POST    → CREATE
PUT     → UPDATE
DELETE  → DELETE
```

---

### 🧠 Key Memory Points

* GET = read only
* POST = create new
* PUT = update existing
* DELETE = remove resource
* One method = one responsibility

---

## 🎥 VIDEO 5 – REST API & Architecture

### ✍️ My Self-Explanation

This video was **very important**.

REST = **Representational State Transfer**

REST API is an **architectural style**, not code.

Main idea:

* Everything is a **resource**
* Communication happens over HTTP
* Data is sent as JSON/XML

Most important concept:
👉 **REST is stateless**

Stateless means:

* Server does not remember clients
* Every request contains all information
* Each request is independent

REST principles:

* Client–Server separation
* Stateless
* Cacheable
* Layered system
* Uniform interface

---

### 🖼️ Diagram – Stateless REST

```
Request 1 → Server → Response
Request 2 → Server → Response
(No memory stored)
```

---

### 🧠 Key Memory Points

* REST is stateless
* Each request is independent
* Improves scalability
* Uses HTTP methods
* RESTful services follow REST rules

---

## 🎥 VIDEO 6 – HTTP vs HTTPS

### ✍️ My Self-Explanation

This video taught me **how data is transferred securely**.

HTTP:

* HyperText Transfer Protocol
* Not secure

HTTPS:

* HTTP + Security
* Uses encryption (SSL/TLS)
* Protects passwords & payments

Both:

* Use client–server model
* Are stateless
* Use same HTTP methods
* Use same status codes

Only difference = **security**.

---

### 🖼️ Diagram – HTTP vs HTTPS

```
HTTP   → Data (plain text ❌)
HTTPS  → Data (encrypted 🔒)
```

---

### 🧠 Key Memory Points

* HTTPS = HTTP with security
* HTTPS encrypts data
* Modern web uses HTTPS
* Required for APIs & login
* Spring Boot apps use HTTPS

---

## 🎥 VIDEO 7 – Status Codes in APIs

### ✍️ My Self-Explanation

This video explained **how server tells result of request**.

Status codes are:

* 3-digit numbers
* Part of HTTP
* Sent with response

They tell:

* Success
* Client error
* Server error

Categories:

* 1xx → Info
* 2xx → Success
* 3xx → Redirect
* 4xx → Client error
* 5xx → Server error

---

### 🖼️ Diagram – Status Code Flow

```
Client
   |
   | Request
   v
Server
   |
   | Response + Status Code
   v
Client understands result
```

---

### 🧠 Key Memory Points

* 200 → OK
* 201 → Created
* 204 → No content
* 400 → Bad request
* 401 → Unauthorized
* 403 → Forbidden
* 404 → Not found
* 500 → Server error

---

## 🎥 VIDEO 8 – Resource, URI & Sub-Resource

### ✍️ My Self-Explanation

This video taught me **how REST APIs are structured**.

A **Resource**:

* Any identifiable data
* Example: user, post, product

A **URI**:

* Identifies a resource
* Example: `/users/1`

A **Sub-resource**:

* Resource inside another resource
* Example: `/users/1/posts/5`

REST APIs use **hierarchy** to stay clean.

---

### 🖼️ Diagram – Resource Hierarchy

```
/users
   |
   |-- /users/{id}
           |
           |-- /users/{id}/posts
                   |
                   |-- /posts/{postId}
```

---

### 🧠 Key Memory Points

* REST is resource-based
* URI identifies resource
* Sub-resources show relationships
* Hierarchy improves scalability
* Spring Boot maps URIs to controllers

---

# 🧠 ONE-LINE RECALL – WHOLE SECTION

> “The web works on client–server communication using HTTP/HTTPS, REST APIs expose resources via URIs using standard HTTP methods, return status codes for every request, and follow stateless, scalable architecture.”
