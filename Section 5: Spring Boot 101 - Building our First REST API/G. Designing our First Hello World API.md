# 🖊️ Designing Our First Hello World API (Spring Boot)

---

## What exactly did I build here?

I built my **first REST API** in Spring Boot.

Meaning:

* If someone hits my app URL with `/hello`
* Spring Boot automatically calls **my method**
* That method returns a response to the browser

No UI.
No HTML.
Just **pure API response**.

---

## URL → Method mapping (core idea)

I defined this rule:

```
domain/hello  →  this Java method runs
```

So Spring Boot is doing:

* Request comes in
* Finds matching mapping
* Executes method
* Sends response back

---

## Understanding `@RestController`

Important realization:

* `@RestController` is **NOT magic**
* It is a **combination of two annotations**

### What it actually contains 👇

```
@RestController
   ↓
@Controller + @ResponseBody
```

Meaning:

* `@Controller` → class can handle HTTP requests
* `@ResponseBody` → return value goes directly to response body

So:

> Whatever I return from method → goes straight to browser

No JSP
No Thymeleaf
No view resolver

---

## Why I used `@RestController` instead of `@Controller`

If I used only `@Controller`:

* Spring expects a **view name**
* It looks for HTML / JSP

But since this is an API:

* I want **raw data**
* So `@RestController` is the correct choice

---

## `@GetMapping` – what did I define?

I used:

```
@GetMapping("/hello")
```

Meaning:

* HTTP method = GET
* URL path = `/hello`

So full URL becomes:

```
http://localhost:8080/hello
```

Spring Boot understands:

> “If GET request comes on `/hello`, call this method”

---

## Running the application – what happened internally?

Steps I observed:

1. I ran `FirstSpringApplication.java`
2. Spring Boot started
3. Embedded **Tomcat server** started automatically
4. Log message appeared:

```
Tomcat started on port 8080
```

Meaning:

* My app is live
* Running locally
* On port 8080

---

## Why Tomcat came without me installing it?

Because:

* `spring-boot-starter-web` dependency
* Includes embedded Tomcat

So:

> No external server setup needed 🚀

---

## Testing in browser – first mistake (important learning)

I opened:

```
http://localhost:8080
```

What happened?

* ❌ White Label Error Page

Why?

* No mapping defined for `/`

Spring Boot was right.

---

## Correct URL testing

Then I tried:

```
http://localhost:8080/hello
```

✅ Success
I saw my response in the browser.

Meaning:

* Controller loaded correctly
* Mapping worked
* API returned response

---

## Flow of Hello World API (VERY IMPORTANT)

```
Browser
   ↓
GET /hello
   ↓
@RestController
   ↓
@GetMapping("/hello")
   ↓
Method executes
   ↓
Return String
   ↓
@ResponseBody
   ↓
Browser shows response
```

---

## What code did I actually write?

Very small code.
But very powerful.

I didn’t:

* Write server config
* Write servlet code
* Configure Tomcat
* Handle HTTP manually

Spring Boot did everything.

---

## Why this is a BIG DEAL (mental note)

Even with:

* 1 annotation
* 1 method
* 1 return statement

I created:

* A running backend service
* A real API
* Production-style architecture

---

## Key understanding I must remember

* `@RestController` = API class
* `@GetMapping` = URL mapping
* Embedded Tomcat runs on port 8080
* `/` ≠ `/hello`
* White label error = no mapping found

---

## 🧠 One-Line Strong Recall (exact style)

> **A Hello World API in Spring Boot is created using @RestController and @GetMapping, where a request to /hello is handled by a mapped method and the returned value is sent directly to the browser via embedded Tomcat running on port 8080.**
