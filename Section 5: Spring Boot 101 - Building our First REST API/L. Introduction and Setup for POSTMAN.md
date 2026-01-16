# 🖊️ Introduction & Setup for POSTMAN

---

## Why did I even need Postman? 🤔

I already created a **POST API** in Spring Boot.

But then I realized:

❌ Browser can easily run **GET**
❌ Browser **cannot properly send POST body**

POST request needs:

* Method = POST
* URL
* **Body (data)**

👉 Browser address bar cannot send body
👉 So I need a **special API testing tool**

---

## Tool name: POSTMAN 🧰

Postman is:

* An **API testing tool**
* Used to **send GET, POST, PUT, DELETE requests**
* Lets me send:

  * Body
  * Headers
  * Authorization
  * Params

👉 Basically: *“Browser for APIs”*

---

## Downloading Postman (what I did)

1. Open browser
2. Search: **Postman**
3. Go to **Postman API Platform**
4. Click:

   ```
   Product → Get started for free
   ```
5. Download version for my OS
   (Windows / Mac / Linux)

📝 Note to self:

* Postman also has **web version**
* Desktop version is more comfortable

---

## First time opening Postman 👀

When I opened Postman, I saw:

### Left side panel:

* **History**

  * Shows all requests I executed earlier

### Right side main area:

* Where I **create & send requests**

---

## Understanding Postman UI (very important 🧠)

```text
+-------------------+-----------------------------+
| History           |  Request Builder            |
| (past requests)   |                             |
|                   |  [GET ▼] http://localhost   |
|                   |                             |
|                   |  Tabs: Params | Auth |      |
|                   |        Headers | Body |     |
|                   |                             |
|                   |        [Send]               |
+-------------------+-----------------------------+
```

---

## Testing GET request in Postman (sanity check ✅)

I already had:

```
GET /hello
```

So I did:

1. Method → **GET**
2. URL → `http://localhost:8080/hello`
3. Click **Send**

📤 Response:

```
Hello World
```

📌 Same output as browser
👉 This confirms my API is running

---

## Switching from GET to POST 🔄

Now real task begins.

Steps I followed:

1. Change method:

   ```
   GET → POST
   ```
2. Keep same URL:

   ```
   http://localhost:8080/hello
   ```

---

## Sending data using POST body 📦

My POST API expects:

```java
@PostMapping("/hello")
public String helloPost(@RequestBody String name)
```

So I **must send body**.

### Steps in Postman:

1. Click **Body**

2. Select **raw**

3. Choose type: **Text**

4. Write body:

   ```
   hello spring boot
   ```

5. Click **Send**

---

## Response I got 🎉

```
Hello hello spring boot!
```

Status Code:

```
200 OK
```

Time:

```
16 ms
```

👉 Means:

* API executed successfully
* Server understood my request
* Returned response correctly

---

## Visual flow (POST request) 📊

```text
Postman
  |
  | POST /hello
  | Body: "hello spring boot"
  ↓
Spring Boot Controller
  |
  | @RequestBody → name
  ↓
return "Hello " + name
  ↓
Postman Response
"Hello hello spring boot!"
```

---

## Status Code 200 – what it means 🟢

`200 OK` means:

* Request reached server
* No error
* Everything worked fine

📝 Later I’ll learn:

* 400 → Bad Request
* 404 → Not Found
* 500 → Server Error

---

## History feature (small but useful 🕒)

Postman automatically saves:

* All GET requests
* All POST requests

So:

* I can quickly re-run them
* No need to type URL again

---

## What I really learned from this video 🎯

* Browser alone is **not enough** for POST
* Postman is used to:

  * Test APIs
  * Send request body
* How to:

  * Switch GET → POST
  * Add raw body
  * Read response & status code
* POST + `@RequestBody` works perfectly with Postman

---

## Common beginner mistakes (noted for future ⚠️)

❌ Forgetting to select **Body → raw**
❌ Sending POST without body
❌ Server not running
❌ Wrong URL or port

---

## 🧠 One-Line Strong Recall (exam / interview ready)

> **Postman is an API testing tool used to execute POST requests by sending request bodies, which cannot be done directly from a browser, allowing us to test Spring Boot REST APIs effectively.**
