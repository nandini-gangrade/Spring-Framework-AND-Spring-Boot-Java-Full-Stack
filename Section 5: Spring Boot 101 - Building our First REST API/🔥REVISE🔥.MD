

# 🧠 Section 5: Spring Boot 101 – Building Our First REST API

So till now, I’ve mainly understood **why Spring Boot exists**.
Earlier Java apps were:

* heavy on configuration
* lots of XML
* slow to start

Spring Boot solves this by:

* giving defaults
* reducing boilerplate
* letting me focus on **business logic**

This section is preparing me to **build real APIs**, not just theory.

---

### 🧠 Diagram

```
Old Spring → XML + Manual Config
Spring Boot → Auto Config + Defaults
```

---

### 🔁 One-line recall

**Spring Boot exists to reduce configuration and help me build production-ready apps faster.**

---

## 📹 B. Introduction to Spring Boot

### ✍️ My understanding

Spring Boot is **not a replacement of Spring**, it is built **on top of Spring**.

What it gives me:

* embedded server (Tomcat)
* starter dependencies
* auto configuration

I don’t need to:

* configure Tomcat
* write XML
* wire beans manually (in most cases)

---

### 🧠 Diagram

```
Spring Boot
   |
   |-- Spring Framework
   |-- Embedded Tomcat
   |-- Auto Configuration
```

---

### 🔁 One-line recall

**Spring Boot is a framework built on Spring that simplifies application setup and development.**

---

## 📹 C. How does Spring Boot work? – Architecture

### ✍️ My understanding

Spring Boot follows **layered architecture**.

Each layer has **one clear responsibility**:

* Controller → talks to user
* Service → business logic
* Repository → database

No layer skips another layer.

---

### 🧠 Diagram

```
Browser / Client
      ↓
Controller (Presentation)
      ↓
Service (Business Logic)
      ↓
Repository (Data Access)
      ↓
Database
```

---

### 🔁 One-line recall

**Spring Boot uses layered architecture: Controller → Service → Repository.**

---

## 📹 D. Getting Started with Spring Initializer

### ✍️ My understanding

Spring Initializr helps me **create a project without manual setup**.

I choose:

* project type (Maven)
* language (Java)
* dependencies (Spring Web)

It generates:

* folder structure
* pom.xml
* main class

---

### 🧠 Diagram

```
Spring Initializr
      ↓
Project Skeleton
      ↓
Ready-to-run App
```

---

### 🔁 One-line recall

**Spring Initializr generates a ready-to-use Spring Boot project with chosen dependencies.**

---

## 📹 E. Setting up Spring Boot Project in IntelliJ

### ✍️ My understanding

IntelliJ reads `pom.xml` and:

* downloads dependencies
* builds project
* prepares run configuration

Main class has:

```
@SpringBootApplication
```

This annotation:

* enables auto config
* component scanning
* starts application

---

### 🧠 Diagram

```
pom.xml → Maven → Dependencies
Main Class → Run → Tomcat Starts
```

---

### 🔁 One-line recall

**Spring Boot apps start from the main class annotated with @SpringBootApplication.**

---

## 📹 F. Let’s Discuss Dependencies

### ✍️ My understanding

Spring Boot uses **starter dependencies**.

Instead of adding many libraries, I add **one starter**.

Example:

* `spring-boot-starter-web` gives:

  * Tomcat
  * Spring MVC
  * Jackson

---

### 🧠 Diagram

```
spring-boot-starter-web
        |
        |-- Tomcat
        |-- MVC
        |-- JSON (Jackson)
```

---

### 🔁 One-line recall

**Starter dependencies bundle commonly used libraries to simplify configuration.**

---

## 📹 G. Designing Our First Hello World API

### ✍️ My understanding

This is my **first real API**.

* `@RestController` → tells Spring this is an API
* `@GetMapping("/hello")` → URL mapping
* method returns response

Browser hits `/hello` → response shown.

---

### 🧠 Diagram

```
Browser → /hello
        → Controller Method
        → Response
```

---

### 🔁 One-line recall

**@RestController with @GetMapping creates REST endpoints in Spring Boot.**

---

## 📹 H. How did our API work?

### ✍️ My understanding

When I run the app:

* Tomcat starts
* DispatcherServlet is created
* Requests are routed to controllers

Spring handles:

* routing
* execution
* response writing

---

### 🧠 Diagram

```
Request
  ↓
DispatcherServlet
  ↓
Controller Method
  ↓
Response
```

---

### 🔁 One-line recall

**DispatcherServlet routes incoming requests to the correct controller method.**

---

## 📹 I. Understanding Spring Boot Auto-Configuration

### ✍️ My understanding

Spring Boot **detects what I added** and configures things automatically.

Examples:

* Tomcat auto-starts
* DispatcherServlet auto-configured
* error pages auto-created

I write **minimum code**, Spring does the rest.

---

### 🧠 Diagram

```
Dependencies → Auto Configuration
No Manual Setup Needed
```

---

### 🔁 One-line recall

**Spring Boot auto-configuration configures components based on classpath dependencies.**

---

## 📹 J. Introduction to application.properties

### ✍️ My understanding

`application.properties` is where I **customize defaults**.

Examples:

* server port
* database config

Properties can be overridden via:

* command line arguments

---

### 🧠 Diagram

```
application.properties
        ↓
Overrides Defaults
```

---

### 🔁 One-line recall

**application.properties customizes Spring Boot’s default configuration.**

---

## 📹 K. Creating a POST Request

### ✍️ My understanding

POST is used when:

* I need to send data
* request body is involved

`@PostMapping`
`@RequestBody` binds body → method variable

---

### 🧠 Diagram

```
POST Request
   ↓
@RequestBody
   ↓
Method
```

---

### 🔁 One-line recall

**POST requests send data to the server using request body.**

---

## 📹 L. Introduction & Setup for Postman

### ✍️ My understanding

Browser cannot send POST body easily.

Postman helps me:

* send GET/POST
* add body, headers
* test APIs

---

### 🧠 Diagram

```
Postman → API → Response
```

---

### 🔁 One-line recall

**Postman is a tool used to test and interact with REST APIs.**

---

## 📹 M. Completing Setup of Postman

### ✍️ My understanding

If I don’t save requests:

* I lose them

Collections help me:

* organize APIs
* reuse requests
* work like a professional

---

### 🧠 Diagram

```
Requests → Collections → Reusable
```

---

### 🔁 One-line recall

**Postman collections help organize and save API requests.**

---

## 📹 N. Getting JSON Response

### ✍️ My understanding

Real APIs return **JSON**, not plain text.

Spring converts:

* Java Object → JSON
  Using:
* Jackson (auto-included)

Getters are important → no getter = no JSON field.

---

### 🧠 Diagram

```
Java Object
   ↓ (Jackson)
JSON Response
```

---

### 🔁 One-line recall

**Spring Boot uses Jackson to automatically convert Java objects to JSON.**

---

## 📹 O. Making use of @PathVariable

### ✍️ My understanding

Path variables make URLs **dynamic**.

Example:

```
/hello/John
```

Spring binds:

* URL part → method variable

Useful for:

* user IDs
* blog slugs
* SEO-friendly URLs

---

### 🧠 Diagram

```
/users/{id}
        ↓
@PathVariable id
```

---

### 🔁 One-line recall

**@PathVariable extracts dynamic values from the URL.**

---

## 📹 P. LAB: Hello Banking API (GET & POST)

### ✍️ My understanding

This lab connects **everything**:

* controller
* GET
* POST
* Postman
* request/response flow

It simulates **real onboarding task**.

---

### 🧠 Diagram

```
Client
 ↓
GET /hello → Welcome Message
 ↓
POST /hello + name → Personalized Message
```

---

### 🔁 One-line recall

**This lab applies GET, POST, request body, and controller concepts in a real-world scenario.**

---

# 🧠🔥 FINAL STRONG RECALL – ENTIRE SECTION

> **Spring Boot simplifies REST API development by providing auto-configuration, embedded servers, and annotation-based programming using layered architecture.**
