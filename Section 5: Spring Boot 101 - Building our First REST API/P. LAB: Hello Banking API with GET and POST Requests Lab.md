
# 📓 LAB: Hello Banking API (GET & POST)

---

## 🏦 Why this lab exists

This lab is **not about banking**.
It is about checking whether I understand:

* How **client talks to server**
* How **Spring Boot receives requests**
* How **GET and POST behave differently**
* How **controllers work**

Banks, startups, and companies **always test this first**.

---

## 🧠 First: What is an API? (very basic)

**API = Application Programming Interface**

In simple words:

> API is a **door** that allows one software to talk to another software.

Example:

* Browser → talks to → Server
* Postman → talks to → Server
* Mobile app → talks to → Server

---

## 🌐 What is a Web API?

A **Web API**:

* Runs on a **server**
* Listens on a **URL**
* Accepts **HTTP requests**
* Sends **HTTP responses**

Example URL:

```
http://localhost:8080/hello
```

---

## 🚦 What is HTTP?

**HTTP = HyperText Transfer Protocol**

It defines:

* How request is sent
* How response is received

Common HTTP methods:

* **GET** → ask for data
* **POST** → send data
* PUT → update
* DELETE → remove

---

## 🎯 Why only GET and POST here?

Because:

* GET = simplest
* POST = introduces request body
* Interviewers expect these first

---

## 🧩 What is Spring Boot?

Spring Boot is a **Java framework** that:

* Runs a web server (Tomcat)
* Handles HTTP requests
* Reduces configuration
* Helps build REST APIs quickly

---

## 📂 What is a Controller?

**Controller** is a Java class that:

> Receives HTTP requests and returns HTTP responses

In Spring Boot:

```java
@RestController
public class HelloController {
}
```

---

## 🧠 New word: `@RestController`

### Definition:

`@RestController` tells Spring:

> “This class will handle REST API requests and return data directly.”

Important:

* No HTML
* No JSP
* Only data (String, JSON, etc.)

---

## 🧠 New word: Annotation

**Annotation** = metadata added to code

Example:

```java
@RestController
```

It **does not execute code**,
It **tells Spring how to behave**.

---

## 🧭 Mapping: How does URL reach method?

Spring uses **mapping annotations**.

---

## 🧠 New word: `@RequestMapping`

### Definition:

`@RequestMapping` maps a **URL path** to a **controller or method**.

Example:

```java
@RequestMapping("/hello")
```

Meaning:

```
Any request starting with /hello comes here
```

---

## 🟢 GET Endpoint — Deep Explanation

### What is GET?

**GET request**:

* Used to **fetch data**
* No request body
* Safe & readable
* Can be tested in browser

---

### Annotation: `@GetMapping`

**Definition**:
`@GetMapping` maps **HTTP GET requests** to a method.

Example:

```java
@GetMapping
public String hello() {
    return "Welcome to Hello Banking API";
}
```

---

### How Spring processes this

Diagram:

```
Browser
   |
   | GET /hello
   |
Spring Dispatcher
   |
Find Controller
   |
Find @GetMapping
   |
Call hello()
   |
Return String
   |
Send Response
```

---

## 🔵 POST Endpoint — Deep Explanation

### What is POST?

**POST request**:

* Used to **send data**
* Data goes in **request body**
* Cannot be tested via browser easily
* Used for create / submit operations

---

## 🧠 New word: Request Body

**Request Body** = data sent **inside the request**, not in URL.

Example:

```
POST /hello
Body: John
```

---

## 🧠 New word: `@PostMapping`

**Definition**:
Maps **HTTP POST requests** to a method.

Example:

```java
@PostMapping
```

---

## 🧠 New word: `@RequestBody`

### Definition:

`@RequestBody` tells Spring:

> “Take the data from request body and put it into this variable.”

Example:

```java
public String greetUser(@RequestBody String name)
```

Spring does:

```
Body → name variable
```

---

## 🧩 Full POST Flow (Very Important)

```
Postman
   |
   | POST /hello
   | Body: John
   |
Spring
   |
Read Body
   |
Bind to String name
   |
Execute method
   |
Return response
```

---

## 🧠 Why browser cannot test POST easily?

Because:

* Browser address bar only supports GET
* POST needs body
* Tools like Postman simulate clients

---

## ⚠️ Common beginner mistakes (Interview gold)

1. Using GET for sending sensitive data ❌
2. Forgetting `@RequestBody` ❌
3. Expecting POST to work in browser ❌
4. Sending `"John"` instead of `John`

---

## 🧠 NAS CONCEPTS (Core Fundamentals)

These are **Non-negotiable concepts** interviewers expect:

### 1. Client–Server Architecture

Client sends request → Server responds

### 2. HTTP Methods

GET vs POST behavior

### 3. Controller Responsibility

Handle requests, return responses

### 4. Request Mapping

How URL reaches method

### 5. Request Body Binding

How data becomes Java variable

---

## 🎤 INTERVIEW: What they will ask

### Q1: What is @RestController?

**Expected Answer**:

> It is used to create REST APIs and return data directly as response.

---

### Q2: Difference between GET and POST?

**Expected Answer**:

> GET is used to fetch data and has no body.
> POST is used to send data in request body.

---

### Q3: Why use @RequestBody?

**Expected Answer**:

> To bind request body data to a method parameter.

---

### Q4: Why POST cannot be tested in browser?

**Expected Answer**:

> Because browser supports only GET through URL bar.

---

### Q5: What does @RequestMapping do?

**Expected Answer**:

> Maps URL paths to controllers or methods.

---

## 🧠 FINAL STRONG RECALL (WRITE THIS 5 TIMES)

> **GET reads data, POST sends data, controllers handle requests, and Spring binds HTTP data to Java using annotations.**

