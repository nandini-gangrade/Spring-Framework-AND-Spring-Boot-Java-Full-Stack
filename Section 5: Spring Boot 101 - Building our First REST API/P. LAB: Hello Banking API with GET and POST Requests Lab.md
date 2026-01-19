
# 📘 LAB GUIDE

## Hello Banking API with GET and POST Requests

---

## 1. Why This Lab Exists (The Real Reason)

This lab is intentionally **simple**, but it is **foundational**.

When you join a company (especially a bank or fintech):

* You are **not trusted with critical systems immediately**
* You are first tested on **fundamentals**
* Your understanding of **standards** matters more than speed

This lab checks whether you understand:

* How **web APIs** work
* How **HTTP** works
* How **Spring Boot** processes requests
* How **clients and servers communicate**

If these basics are weak, **advanced topics will collapse**.

---

## 2. The Real-World Simulation

You are asked to **imagine** this scenario:

* You joined a **digital banking platform**
* You are in your **first few days**
* Your manager gives you a **starter task**

Why this story?

Because real companies:

* Onboard developers gradually
* Give **safe, non-critical tasks**
* Observe *how you approach a problem*

This is not about “Hello”.
This is about **thinking like a backend engineer**.

---

## 3. Understanding the Requirements (Slowly)

### Requirement 1: GET Endpoint

* Endpoint path:

  ```
  /hello
  ```
* HTTP method:

  ```
  GET
  ```
* Controller:

  ```
  HelloController
  ```
* Response:

  ```
  Welcome to Hello Banking API
  ```

This endpoint:

* Takes **no input**
* Returns a **simple message**
* Is used to verify the API is reachable

---

### Requirement 2: POST Endpoint

* Endpoint path:

  ```
  /hello
  ```
* HTTP method:

  ```
  POST
  ```
* Input:

  * `name` (sent in request body)
* Output:

  ```
  Hello <name>, welcome to Hello Banking API
  ```

This endpoint:

* Accepts **data from client**
* Returns a **customized response**

---

### Important Observation

The **URL is the same**:

```
/hello
```

But the **HTTP method is different**.

This is a **core REST concept**:

> Same resource, different actions.

---

## 4. Core Concepts (With Definitions)

Before coding, we must understand the language of backend development.

---

### 4.1 API (Application Programming Interface)

**Definition**:
An API is a controlled way for one software system to interact with another.

**Why APIs exist**:

* Users should not access databases directly
* APIs enforce rules, security, and structure
* APIs act as a **middle layer**

---

### 4.2 Web API

A **Web API**:

* Uses the **HTTP protocol**
* Is accessed using **URLs**
* Can be called by browsers, mobile apps, or servers

Example:

```
http://localhost:8080/hello
```

---

### 4.3 HTTP (HyperText Transfer Protocol)

**HTTP** is a set of rules that define:

* How requests are sent
* How responses are returned
* What actions are allowed

It is **stateless**, meaning:

* Each request is independent
* Server does not remember previous requests by default

---

### 4.4 HTTP Request

A **request** is sent from a **client** to a **server**.

It contains:

* HTTP method (GET, POST, etc.)
* URL
* Headers (metadata)
* Body (optional data)

---

### 4.5 HTTP Response

A **response** is sent from a **server** to a **client**.

It contains:

* Status code (200, 400, 404, etc.)
* Headers
* Body (actual result)

---

### 4.6 Client

A **client** is any system that sends HTTP requests.

Examples:

* Browser
* Postman
* Mobile application
* Frontend application (React, Angular)

---

### 4.7 Server

A **server**:

* Listens for requests
* Processes logic
* Sends responses

In this lab, the server is a **Spring Boot application**.

---

## 5. What Is Spring Boot?

**Spring Boot** is a Java framework that:

* Simplifies backend development
* Automatically configures components
* Includes an embedded web server

Why companies use it:

* Faster development
* Industry standard
* Easy integration
* Scalable

---

## 6. Project Setup (Why Each Step Matters)

### ZIP File

The ZIP file contains:

* Source code
* Configuration files
* Build instructions

This mimics:

> “Cloning a company repository”

---

### pom.xml (Project Object Model)

**pom.xml**:

* Defines dependencies (Spring Web, etc.)
* Specifies Java version
* Tells Maven how to build the project

Without `pom.xml`, the project cannot run.

---

### IntelliJ IDEA

An **IDE (Integrated Development Environment)**:

* Helps write code
* Manages dependencies
* Runs and debugs applications

---

### Opening pom.xml as Project

This tells IntelliJ:

* This is a Maven project
* Download required libraries
* Set correct classpath

---

## 7. Running the Application

### Main Class

The main class contains:

```java
@SpringBootApplication
```

This annotation:

* Starts the Spring container
* Scans components
* Starts the embedded web server

---

### Embedded Tomcat

**Tomcat** is a web server that:

* Listens on port 8080
* Accepts HTTP requests
* Forwards them to Spring

Spring Boot embeds Tomcat so manual setup is not required.

---

## 8. Controller Fundamentals

### What Is a Controller?

A **controller**:

* Receives HTTP requests
* Contains request-handling logic
* Returns responses

It is the **entry point** of an API.

---

### @RestController

**@RestController** is an annotation.

**Annotation** = metadata that guides Spring behavior.

`@RestController` tells Spring:

* This class exposes REST APIs
* Return values go directly to response body
* No UI rendering

---

## 9. URL Mapping Concepts

### Request Mapping

**Request mapping** connects:

```
URL → Java method
```

Spring must know:

> “Which method handles which request?”

---

### @RequestMapping

Used to map a path:

```java
@RequestMapping("/hello")
```

Meaning:

* All requests starting with `/hello` are handled here

Why use it at class level?

* Avoid repetition
* Cleaner structure
* Standard practice

---

## 10. GET Endpoint (Deep Explanation)

### What Is GET?

GET is used to:

* Retrieve data
* Perform read-only operations

Characteristics:

* No request body
* Safe (does not change server state)
* Can be cached
* Can be tested in browser

---

### @GetMapping

A specialized annotation for GET requests.

Why it exists:

* Improves readability
* Reduces boilerplate
* Makes intent clear

---

### GET Method Implementation

```java
@GetMapping
public String hello() {
    return "Welcome to Hello Banking API";
}
```

Explanation:

* `public`: accessible to Spring
* `String`: response body
* Returned value is sent directly to client

---

### Browser Testing

Browsers can test GET because:

* Address bar sends GET requests
* No request body is needed

---

## 11. POST Endpoint (Deep Explanation)

### What Is POST?

POST is used to:

* Send data to server
* Create or submit information

Characteristics:

* Has a request body
* Not safe
* Not idempotent
* Cannot be tested via browser address bar

---

### Request Body

The **request body** holds actual data.

Example:

```
POST /hello
Body: John
```

---

### @PostMapping

Maps POST requests to a method.

Purpose:

* Clearly indicates POST behavior
* Improves code readability

---

### @RequestBody

`@RequestBody` tells Spring:

* Read data from request body
* Convert it to a Java type
* Assign it to a variable

```java
public String greetUser(@RequestBody String name)
```

---

### POST Request Flow

1. Client sends POST request
2. Server reads body
3. Spring binds body to variable
4. Method executes
5. Response is returned

---

## 12. Why Postman Is Needed

Browsers:

* Cannot send request body easily

Postman:

* Simulates real clients
* Sends POST, PUT, DELETE requests
* Used widely in industry

---

## 13. Common Beginner Pitfalls

* Using GET to send data
* Forgetting `@RequestBody`
* Expecting POST to work in browser
* Sending quoted strings unintentionally

---

## 14. What This Lab Actually Teaches

This lab builds understanding of:

* HTTP fundamentals
* REST design
* Spring Boot request handling
* Client-server communication
* Clean API structure

---

# 15. Interview Perspective (MOST IMPORTANT)

This section explains **how interviewers think**, not Q&A.

---

## What Interviewers Are Evaluating

### 1. Conceptual Understanding (Not Syntax)

They want to see:

* Do you understand *why* GET and POST exist?
* Do you know *where* data goes?
* Can you explain request flow clearly?

Memorized answers are obvious and rejected.

---

### 2. HTTP & REST Fundamentals

They expect:

* Correct HTTP method usage
* Understanding of stateless communication
* Awareness of API standards

---

### 3. Backend Thinking

They look for:

* Clean separation of concerns
* Correct annotation usage
* Ability to build on fundamentals

This lab is the **foundation** for:

* Path variables
* Query parameters
* JSON payloads
* DTOs
* Validation
* Security

---

### 4. Maturity Level

A beginner says:

> “It works.”

A good candidate says:

> “This is why it works and why it’s designed this way.”

---

## Final Recall Line (Write This)

> **This lab proves I understand how HTTP works, how Spring maps requests to code, and why REST APIs are designed the way they are — not just how to write them.**
