## Why this video exists

Till now I learned:

* loose coupling
* IoC
* DI
* beans

But one big question was still open in my head:

> **Who actually does all this work at runtime?**

Answer: **Spring Container**
And this video explains **what it is, what types it has, and how it knows what to manage**.

---

## Video 1: Spring Container — What it is

### What I understood (explaining to myself)

A **Spring Container** is basically a manager.

I can think of it as a **box** that:

* creates objects
* stores objects
* injects objects where needed
* manages their lifecycle

These objects are the **beans**.

---

### Simple mental diagram

```
+----------------------+
|   Spring Container   |
|----------------------|
|  Bean 1              |
|  Bean 2              |
|  Bean 3              |
|  Bean 4              |
+----------------------+
```

My application code does **not** create these objects.
It just asks for them when needed.

---

### What the container actually does

* Instantiates beans
* Maintains them
* Injects dependencies
* Controls lifecycle (create → use → destroy)

So whenever some class needs another object, **container supplies it**.

---

## Video 2: Types of Spring Container

### Two types I need to remember

Spring provides **two containers**:

1. **BeanFactory**
2. **ApplicationContext**

---

### BeanFactory (basic one)

* Oldest and simplest container
* Only does **basic dependency injection**
* Lightweight

Think of it as:

> “Just enough to get objects wired together.”

---

### ApplicationContext (the one we actually use)

* More advanced than BeanFactory
* Includes:

  * dependency injection
  * event handling
  * internationalization
  * resource loading

In real projects:

> **Almost everyone uses ApplicationContext**

---

### Diagram: BeanFactory vs ApplicationContext

```
BeanFactory
   |
   |-- basic DI
   |
ApplicationContext
   |
   |-- DI
   |-- Events
   |-- Resource handling
   |-- Extra features
```

Interview-safe line:

> ApplicationContext is a superset of BeanFactory.

---

## Video 3: Configuration — how container knows what to manage

### The big question answered

> How does Spring Container know **which objects** to manage?

Answer:

> **Configuration**

Spring does nothing by guessing.
We must **tell it explicitly**.

---

### My role as a developer

I must tell Spring:

* which classes should be managed
* which ones are beans

I do this using **configuration**.

---

### Diagram: Configuration → Container

```
Configuration
   |
   |-- Bean definitions
   v
Spring Container
   |
   |-- creates & manages beans
```

---

## Video 4: What configuration actually contains

### Key takeaway

Configuration contains **bean definitions**.

---

### What is a bean definition?

A bean definition tells Spring:

* which class to create
* how to create it
* that it should be managed

In simple words:

> “Spring, please take responsibility for this object.”

---

### Important rule (must remember)

❌ No bean definition
→ ❌ Spring won’t manage it

✅ Bean definition present
→ ✅ Spring container manages it

---

### High-level flow (very important)

```
Configuration file
       ↓
Bean Definitions
       ↓
Spring Container
       ↓
Managed Beans
       ↓
Dependency Injection at runtime
```

---

## How this connects to everything I learned earlier

* **Loose coupling** → achieved using interfaces
* **DI** → dependencies passed, not created
* **IoC** → Spring controls object creation
* **Beans** → objects Spring manages
* **Container** → the thing doing all of this
* **Configuration** → instructions given to container

Everything fits together cleanly.

---

## One-line final recall (for revision)

> **Spring Container manages the lifecycle and dependency injection of beans based on configuration that defines which objects Spring should manage.**
