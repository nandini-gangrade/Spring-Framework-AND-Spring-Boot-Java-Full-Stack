## 4️⃣ @Value Annotation (Injecting values into components)

---

## What problem this video is solving (why we need @Value)

Till now:

* We created a **component**
* We enabled **component-scan**
* Spring successfully created the bean

BUT…

When we printed the object, we saw:

```
firstName = null
lastName = null
salary = 0.0
```

So the question is:

> **How do I put values inside my component properties without XML?**

👉 Answer: **@Value annotation**

---

## What is @Value (in simple words)

`@Value` is an annotation that lets us:

> **Inject (put) some value directly into a variable**

Think of it like:

> “Spring, please put THIS value here when creating the object.”

📦 Package:

```
org.springframework.beans.factory.annotation
```

---

## Basic example – Injecting a simple value

Suppose I have:

```
private String firstName;
```

Now I write:

```
@Value("Hello")
private String firstName;
```

What happens?

* Spring creates Employee object
* It sees `@Value("Hello")`
* It assigns `"Hello"` to `firstName`

So now output becomes:

```
firstName = Hello
```

Earlier it was `null`, now it has a value ✅

---

## Important understanding (very important)

* `@Value` works **only because Spring is creating the object**
* If I use `new Employee()` → ❌ won’t work
* Must be a **Spring-managed bean**

---

## Injecting system properties (real-world useful)

Instead of hardcoding values, we can inject **system values**.

Example:

```
@Value("${java.home}")
private String lastName;
```

What is `${java.home}`?

* It’s a **system property**
* It contains Java installation path

So Spring does this:

```
lastName = System.getProperty("java.home")
```

Output becomes something like:

```
lastName = /usr/lib/jvm/java-17
```

🔥 This is very useful in real projects.

---

## Injecting expressions (calculated values)

Spring also supports **expressions**.

Syntax:

```
#{ expression }
```

Example:

```
@Value("#{4 * 4}")
private double salary;
```

What happens?

* Spring evaluates `4 * 4`
* Result = `16`
* Assigns it to `salary`

So output:

```
salary = 16.0
```

This is called **SpEL (Spring Expression Language)**
(No need to remember name now, just idea)

---

## Types of values you can inject using @Value

You can inject:

1️⃣ Hardcoded values

```
@Value("Ali")
```

2️⃣ Numbers

```
@Value("100")
```

3️⃣ System properties

```
@Value("${java.home}")
```

4️⃣ Expressions

```
@Value("#{10 + 20}")
```

---

## Diagram – How @Value works internally

```
Spring Container
      |
      |-- Creates Employee Bean
              |
              |-- @Value("Hello") → firstName = "Hello"
              |-- @Value("${java.home}") → lastName = Java path
              |-- @Value("#{4*4}") → salary = 16
```

---

## Why @Value is useful (in real projects)

* Set **default values**
* Read **environment variables**
* Inject **config values**
* Avoid XML property injection

Later, same concept will be used with:

* `application.properties`
* `application.yml`

---

## Final Understanding (talking to myself)

> “@Value helps me inject values directly into my Spring bean variables without writing XML, and Spring automatically fills them when creating the object.”

---

## 🧠 One-Line Recall

> **@Value annotation is used to inject default, system, or computed values into Spring-managed bean properties.**
