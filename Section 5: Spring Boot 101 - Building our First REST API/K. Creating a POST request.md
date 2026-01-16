

## Step 0: Resetting things (important)

First thing I did:

* I **removed** this line from `application.properties`:

```
server.port=1990
```

Why?

👉 Because I want Spring Boot to run on **default port 8080**
👉 Less confusion while testing

So now:

```
App URL → http://localhost:8080
```

---

## Where am I writing POST logic? 📍

Inside:

```
HelloController
```

This is already:

* A `@RestController`
* Handling requests

I already had a **GET request** here.

Now I want to create a **POST request**.

---

## First: Understanding POST vs GET (very important 🧠)

### GET request:

* Used to **fetch data**
* Usually no body
* Example:

```
GET /hello
```

### POST request:

* Used to **send data**
* Has a **request body**
* Example:

```
POST /hello
Body → "Nandini"
```

👉 POST is used when:

* Sending form data
* Sending JSON
* Creating resources

---

## Creating a POST mapping 🚀

For GET we used:

```
@GetMapping("/hello")
```

So logically for POST we use:

```
@PostMapping("/hello")
```

Spring Boot is very readable like this 👍

---

## Writing the POST method (basic)

```java
@PostMapping("/hello")
public String helloPost() {
    return "Hello!";
}
```

This is valid, but boring 😄
I want to send **data from client** and use it.

---

## Problem: Where does user input come from? 🤔

I want something like:

```
Hello Nandini!
```

But right now:

* `name` does not exist
* Java throws error

So I need:
👉 A way to **accept data from POST request**

---

## Solution: `@RequestBody` annotation 🧩

I added this:

```java
public String helloPost(@RequestBody String name)
```

### What does `@RequestBody` mean?

In my own words:

> “Spring Boot, please take the data sent inside the POST request body and put it into this variable.”

So if client sends:

```
Nandini
```

Then:

```
name = "Nandini"
```

---

## Final POST method code ✅

```java
@PostMapping("/hello")
public String helloPost(@RequestBody String name) {
    return "Hello " + name + "!";
}
```

---

## Full flow in simple English 🧠

1. Client sends POST request to `/hello`
2. Request has body (example: `"Aman"`)
3. Spring Boot:

   * Reads request body
   * Stores it in `name`
4. Method runs
5. Response is returned

---

## Visual diagram of POST flow 📊

```text
Client (Postman)
   |
   | POST /hello
   | Body: "Aman"
   ↓
@Controller
@PostMapping("/hello")
@RequestBody → name="Aman"
   ↓
return "Hello Aman!"
   ↓
Response sent back
```

---

## Why browser alone is NOT enough ❌🌐

Browsers:

* Can easily do GET
* Cannot easily send POST body

So:

```
localhost:8080/hello
```

❌ Cannot send POST data properly

---

## Tool needed: Postman 🧰

To test POST requests, we use tools like:

* Postman
* Insomnia
* curl

Postman allows:

* Choose HTTP method (POST)
* Add request body
* See response

---

## What I learned in this video 🎯

* How to define POST mapping
* Difference between GET & POST
* How data is sent using request body
* What `@RequestBody` does
* Why Postman is required

---

## Common beginner confusion (clearing it now 🚨)

❓ *Why GET didn’t need parameters?*
👉 GET usually fetches data, no body

❓ *Can POST send JSON later?*
👉 Yes, very common (we’ll do that soon)

❓ *Is `@RequestBody` mandatory for POST?*
👉 If you want data from body → YES

---

## 🧠 One-Line Strong Recall

> **A POST request in Spring Boot is created using `@PostMapping`, and data sent from the client is received inside the controller method using `@RequestBody`, allowing the application to process user-provided input.**

