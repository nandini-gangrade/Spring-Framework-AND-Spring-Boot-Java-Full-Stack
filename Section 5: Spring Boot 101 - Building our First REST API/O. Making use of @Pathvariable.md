Alright.
Below is **“me explaining to myself so I don’t forget”** style notes.
Read it slowly like a handwritten notebook 📓.

---

# 📓 Path Variable (@PathVariable) — Self Notes

### Topic: Making URLs dynamic in Spring Boot (GET request)

---

## 🤔 What am I learning?

I am learning **Path Variable**.

Path Variable means:
👉 *Passing a value directly inside the URL*
👉 *That value can change (dynamic)*

---

## 🐢 Slow start — what problem am I solving?

Normally, I have a GET API like this:

```
/hello
```

This URL is **fixed**.
No matter who calls it, response is always same.

But sometimes I want this 👇
I want the **URL to change based on input**.

Example:

```
/hello/John
/hello/Michael
/hello/Tom
```

And response should change based on the name.

---

## 🔁 Why do I need this?

Because real applications need **dynamic data**.

Examples I already see on internet:

```
/users/1
/users/2
```

```
/blog/ecommerce-business-ideas
/blog/digital-marketing-tips
```

Only **one part changes**, rest is same.

---

## 🧠 Key idea (very important)

👉 **Part of URL can be dynamic**
👉 Spring Boot lets me catch that part
👉 Using **@PathVariable**

---

## ✍️ How do I write a dynamic URL?

### Step 1: Define URL with template

I tell Spring:

> “This part is dynamic”

I do this using **curly braces `{}`**

Example:

```
/hello/{name}
```

Here:

* `hello` → fixed
* `{name}` → dynamic

---

## ✍️ Step 2: Capture it in method

I use **@PathVariable**

```
@GetMapping("/hello/{name}")
public String helloParam(@PathVariable String name) {
    return "Hello " + name;
}
```

---

## 🧩 What is happening internally?

Diagram time ⬇️

```
URL typed by user:
-------------------
/hello/John

Mapping:
--------
/hello/{name}

Binding:
--------
{name} → "John"

Method receives:
----------------
String name = "John"

Response:
---------
Hello John
```

---

## 🧪 Testing in browser

If I type:

```
http://localhost:8080/hello/John
```

Response:

```
Hello John
```

If I type:

```
/hello/Michael
```

Response:

```
Hello Michael
```

👉 Whatever I pass → I get back.

---

## 📌 Important definition (simple words)

**@PathVariable** is an annotation in Spring MVC that:

* Reads values from URL
* Binds them to method parameters
* Works with URI template variables

---

## 🔗 Fixed + Dynamic together

I can mix **fixed** and **dynamic** parts.

Example:

```
/hello/{name}/show
```

Diagram:

```
/hello/John/show
  |     |     |
 fixed dynamic fixed
```

Only `{name}` changes.

---

## ❌ Common mistake (note to self)

⚠️ Variable name must MATCH.

This is correct:

```
/hello/{name}
@PathVariable String name
```

❌ This will NOT work:

```
/hello/{name}
@PathVariable String name1
```

Names must be SAME.

---

## 🌍 Real-world use cases

* `/users/{id}` → get user by ID
* `/products/{productId}`
* Blog URLs for SEO
* Clean and readable URLs

---

## 🧠 Final Recall Line (VERY IMPORTANT)

> **If I forget everything else, remember this:**
> **@PathVariable lets me capture a dynamic part of the URL and use it inside my method.**
