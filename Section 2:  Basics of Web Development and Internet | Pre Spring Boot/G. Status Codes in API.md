## 1️⃣ Why Do We Need Status Codes? (VERY IMPORTANT – WHY FIRST)

When humans communicate:

* We say **“Okay”**
* Or **“There is a problem”**

Software systems need the **same kind of acknowledgement**.

👉 When a client sends a request to a server:

* How does it know if it worked?
* How does it know what went wrong?

📌 **Status codes are that acknowledgement.**

Without status codes:

* Client wouldn’t know success or failure
* Debugging would be impossible
* APIs would be unreliable

---

## 2️⃣ What Are Status Codes?

### 🔹 Simple Definition

**Status codes are 3-digit numbers** sent by the server to indicate the **result of an HTTP request**.

📌 They are part of the **HTTP protocol**.

---

### 🔹 What Do Status Codes Tell Us?

They tell:

* Was the request successful?
* Was there an error?
* Who made the mistake? (client or server)
* What action should be taken next?

---

## 3️⃣ Real-World API Communication Example

### Scenario:

* Cloud Server (Backend)
* Two clients:

  * Mobile App
  * Desktop / Browser App

---

### Diagram – API Communication with Status Code

```
Mobile App        Desktop App
     |                 |
     | Request         | Request
     v                 v
        Cloud Server
              |
              | Response + Status Code
              v
        Client understands result
```

📌 Response **always comes with a status code**.

---

## 4️⃣ Why Status Codes Are Critical

Even if you get a response:

* Was it successful?
* Was data created?
* Was authentication missing?
* Did server crash?

👉 **Status code answers these questions instantly.**

---

## 5️⃣ Structure of Status Codes

### 🔹 Key Rule

* Status codes are **3-digit numbers**
* **First digit = category**
* Last two digits = specific meaning

📌 Example:

* `404` → Category `4` (Client Error)

---

## 6️⃣ Classification of Status Codes

There are **5 main categories**:

---

### 🔹 1xx – Informational

* Request received
* Processing is continuing

📌 Rarely used directly in REST APIs

---

### 🔹 2xx – Successful

Meaning:

> Request was received, understood, and processed successfully

📌 This is what you WANT most of the time.

---

### 🔹 3xx – Redirection

Meaning:

> Client must take further action

Example:

* Resource moved to another URL

---

### 🔹 4xx – Client Error

Meaning:

> Client made a mistake

Examples:

* Wrong URL
* Bad request format
* Missing authentication

📌 **Your fault as client**

---

### 🔹 5xx – Server Error

Meaning:

> Server failed to process valid request

Examples:

* Server crash
* Unhandled exception
* Database down

📌 **Server’s fault**

---

### Diagram – Status Code Categories

```
1xx → Informational
2xx → Success ✅
3xx → Redirect
4xx → Client Error ❌
5xx → Server Error 💥
```

---

## 7️⃣ Commonly Used Status Codes (VERY IMPORTANT)

These are **must-remember**.

---

### ✅ 200 OK

* Request successful
* Most common status code

📌 Example:

* Fetch users
* Fetch products

---

### ✅ 201 Created

* Resource created successfully

📌 Example:

* New user created
* New product added

---

### ✅ 204 No Content

* Request successful
* Nothing to return

📌 Example:

* Delete operation
* Update without response body

---

### 🔁 301 Moved Permanently

* Resource URL has changed

📌 Example:

* Old API URL replaced by new one

---

### ❌ 400 Bad Request

* Client sent invalid request
* Wrong syntax or parameters

📌 Example:

* Missing required field
* Invalid JSON format

---

### 🔐 401 Unauthorized

* Authentication missing or invalid

📌 Example:

* API requires token
* Client didn’t send token

---

### 🚫 403 Forbidden

* Authenticated but not allowed

📌 Example:

* User role not permitted

---

### 🔍 404 Not Found

* Resource does not exist

📌 Example:

* Invalid URL
* Wrong ID

---

### 💥 500 Internal Server Error

* Server crashed or exception occurred

📌 Example:

* Null pointer exception
* Database error

---

## 8️⃣ Client vs Server Errors (VERY CLEAR DIFFERENCE)

| Code Type | Meaning      | Fault  |
| --------- | ------------ | ------ |
| 4xx       | Client error | Client |
| 5xx       | Server error | Server |

📌 This distinction is **critical in debugging**.

---

## 9️⃣ Status Codes + REST APIs

REST APIs:

* Always return status codes
* Follow HTTP standards

📌 Status codes make REST APIs:

* Predictable
* Reliable
* Easy to debug

---

## 🔗 How This Connects to Spring Boot (Preview)

In Spring Boot:

* You control status codes
* You return meaningful responses

---

### Spring Boot Example

```java
@PostMapping("/users")
public ResponseEntity<User> createUser(@RequestBody User user) {
    User savedUser = userService.save(user);
    return new ResponseEntity<>(savedUser, HttpStatus.CREATED);
}
```

📌 Returns:

* **201 Created**

---

### Another Example

```java
@GetMapping("/users/{id}")
public ResponseEntity<User> getUser(@PathVariable Long id) {
    return userRepository.findById(id)
        .map(user -> ResponseEntity.ok(user))
        .orElse(ResponseEntity.notFound().build());
}
```

📌 Returns:

* **200 OK** or **404 Not Found**

---

## 🧠 VIDEO 7 – MASTER KEY TAKEAWAYS (HAND NOTES – WRITE THESE)

✍️ These are **high-recall bullets** — write them properly:

* APIs need acknowledgement for requests
* Status codes indicate request result
* Status codes are part of HTTP protocol
* Status codes are 3-digit numbers
* First digit defines response category
* 1xx → Informational
* 2xx → Successful responses
* 3xx → Redirection responses
* 4xx → Client-side errors
* 5xx → Server-side errors
* 200 means request successful
* 201 means resource created
* 204 means success with no content
* 301 means resource moved permanently
* 400 means bad request from client
* 401 means authentication required
* 403 means access forbidden
* 404 means resource not found
* 500 means server error
* Status codes help debugging and clarity
* Spring Boot APIs use status codes extensively

---

## 🧩 One-Line Recall (Interview / Revision)

> “HTTP status codes are three-digit numbers used by APIs to indicate whether a client request was successful, failed, or caused an error.”

---

**Thank you**

---

👉 Next video?
Say **“Resource, URI and Sub-Resource”** and we continue 🚀
