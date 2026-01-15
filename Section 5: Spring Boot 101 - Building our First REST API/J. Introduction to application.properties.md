
# 🖊️ Introduction to `application.properties`

---

## First thing I noticed in the project 📁

Inside:

```
src → main → resources
```

There is a file called:

```
application.properties
```

This file already exists — I didn’t create it.

That itself tells me:

> Spring Boot **expects** this file and **looks for it automatically**.

---

## So what exactly is `application.properties`? 🤔

In my own words:

> `application.properties` is the **central configuration file** of a Spring Boot application.

Spring Boot already gives me:

* Default configuration
* Sensible values (like port 8080)

This file allows me to:
👉 **override those defaults**
👉 **customize behavior without touching code**

---

## How configuration works conceptually 🧠

Spring Boot has:

* Auto-configuration
* Predefined defaults

`application.properties` is my way of saying:

> “Hey Spring Boot, I like your defaults,
> but for *this project*, do it *my way*.”

---

## Format of application.properties

It works on **key = value** pairs.

Example:

```
server.port=1990
```

Left side → *what to configure*
Right side → *what value I want*

---

## Where do these keys come from? 🤷

I don’t invent keys randomly.

They come from:

* Spring Boot’s official configuration properties

That’s why we searched:

```
application properties spring boot
```

And opened the **official documentation**.

---

## `.properties` vs `.yaml`

Spring Boot supports:

* `application.properties`
* `application.yml` / `application.yaml`

Both do the same thing.

In this course / learning:
👉 We stick to **`.properties`** (simpler, flat structure)

---

## Understanding `server.port` (very important)

By default:

```
Spring Boot → port 8080
```

I confirmed this when:

```
Tomcat started on port 8080
```

Now I changed it:

```
server.port=1990
```

### What happened after restart?

* Tomcat started on **1990**
* 8080 stopped working
* App moved completely to new port

👉 This proves:

> Spring Boot **reads application.properties at startup**

---

## Important rule 🚨

Changes in `application.properties`:

* ❌ Do NOT apply instantly
* ✅ Apply **only after restart**

Always restart the app after changes.

---

## Visual: How port configuration flows

```text
application.properties
        ↓
server.port=1990
        ↓
Spring Boot startup
        ↓
Embedded Tomcat
        ↓
Application runs on port 1990
```

---

## Why browser behaved the way it did 🌐

* `localhost:8080` → ❌ Not reachable
* `localhost:1990/hello` → ✅ Works

Because:

> The server itself moved, not just the endpoint.

---

## application.properties is NOT only for server config

This file can configure **almost everything**:

* Server
* Database
* Security
* Logging
* JPA
* Caching
* Actuators

Basically:

> Anything Spring Boot auto-configures
> can be customized here.

---

## Database configuration example (real-world important)

Example MySQL config:

```
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=root
spring.datasource.password=admin
spring.jpa.hibernate.ddl-auto=update
```

### What this tells Spring Boot:

* Which database to connect to
* Credentials
* How to manage schema

---

## Understanding `ddl-auto=update` (simple meaning)

```
update = 
- create tables if not exist
- update schema if changed
```

Spring Boot + Hibernate:

* Automatically sync Java entities with DB

(Extremely powerful, but must be used carefully in production)

---

## One BIG concept: overriding hierarchy ⚡

Spring Boot follows **priority order**.

Higher priority overrides lower ones.

Example:

* application.properties → lower
* command line arguments → higher

So if I run:

```
--server.port=7070
```

Then:

* `application.properties` says 1990
* Command line says 7070
* 👉 App runs on **7070**

---

## Visual: Configuration priority

```text
Command Line Args  (Highest)
        ↓
application.properties
        ↓
Spring Boot Defaults (Lowest)
```

---

## Why this is powerful in real projects 🧠

Same codebase, different environments:

* Dev → port 8080
* QA → port 9090
* Prod → port 80

Only config changes.
No code changes.

---

## What I should always remember 📌

* `application.properties` is read at startup
* It overrides Spring Boot defaults
* Uses key=value format
* Controls almost everything
* Can be overridden externally

---

## 🧠 One-Line Strong Recall

> **`application.properties` is the central configuration file in Spring Boot that allows developers to override default auto-configuration values using key-value pairs, enabling environment-specific customization without changing application code.**


