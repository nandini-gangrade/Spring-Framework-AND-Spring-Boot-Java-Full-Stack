# 🖊️ Section 3: Spring Framework – The Basics (Before Spring Boot)

---

## A. What is a Web Framework?

Okay, so before frameworks, building a web app was a nightmare. I had to write **servlet code**, handle requests, responses, and all the boilerplate every single time.

A **web framework** is like a **helper**. It handles the repetitive stuff for me so I can focus on **business logic**.

* Think Spring: It sits between the **browser** and **my code**.
* Without it, I’d manually handle routing, requests, responses, objects… ugh.

**Diagram (mental picture)**

```
Browser
   |
   v
Web Framework
   |
   v
My Business Logic
```

**One-line recall:**

> Web framework = middle helper that removes boilerplate and speeds up web app development.

---

## B. Introduction to Spring Framework

Spring is **lightweight** and **modular**.

* It does **not force me** to extend special classes or implement weird interfaces.
* It focuses on **IoC** (Inversion of Control) and **DI** (Dependency Injection).
* Spring manages objects (beans) for me.

**Diagram**

```
Spring Container
   |
Creates & manages
   |
Beans (objects)
```

**One-line recall:**

> Spring is a framework that manages objects and dependencies so I don’t have to.

---

## C. Tight Coupling and Loose Coupling

Tight coupling = class directly creates another class → bad.

Example:

```
Car ---> new Engine()
```

Problem: Hard to change engine type, hard to test.

Loose coupling = class depends on **interface** → good.

```
Car ---> Engine (interface)
         |-- PetrolEngine
         |-- DieselEngine
```

Benefit: I can swap implementations easily, test easier, code flexible.

**One-line recall:**

> Loose coupling makes code flexible, testable, and change-friendly.

---

## D. Hands-On: Tight & Loose Coupling

So when I tested:

* **Tight coupling**: changing implementation broke my code.
* **Loose coupling**: I could just switch the implementation bean; Car didn’t care.

Use interfaces and dependency injection → **future-proof design**.

**Diagram**

```
Car --> Engine (interface)
         |-- PetrolEngine
         |-- DieselEngine
```

**One-line recall:**

> Interfaces + external injection = safe, flexible design.

---

## E. Core Concepts of Spring

Spring revolves around:

1. **IoC (Inversion of Control)** – Spring creates objects instead of me.
2. **DI (Dependency Injection)** – Spring provides dependencies.
3. **Bean** – object managed by Spring.
4. **Container** – manages all beans and their lifecycle.

**Diagram**

```
Me ❌ creates objects
Spring ✅ creates objects & injects dependencies
```

**One-line recall:**

> Spring controls object creation and wiring via IoC and DI.

---

## F. Spring Container & Configuration

The **container** is Spring’s brain.

* Reads configuration (XML, Java, annotations)
* Creates beans
* Injects dependencies

**Diagram**

```
Configuration (XML)
      |
Spring Container
      |
Beans ready to use
```

**One-line recall:**

> Spring Container reads config and manages all beans automatically.

---

## G. Setting Up a Spring Project

Steps:

1. Create project
2. Add Spring dependencies
3. Create configuration file (XML)
4. Load container in main class
5. Request beans

**Diagram**

```
Main class
   |
Load XML config
   |
Spring Container → Bean
```

**One-line recall:**

> Spring project starts by loading container + configuration so beans are ready.

---

## H. Creating Your First Bean

A **bean** = object managed by Spring.

* Declared with `<bean>` in XML
* Spring creates it, stores it, and injects it wherever needed

**Diagram**

```
<bean id="car" class="Car"/>
        |
Spring creates Car object
```

**One-line recall:**

> Bean = object whose lifecycle Spring fully manages.

---

## I. Lifecycle of a Spring Bean

Bean lifecycle steps:

1. Bean object created
2. Dependencies injected
3. **Init method** called
4. Bean ready to use
5. **Destroy method** called

Spring manages the full lifecycle, I don’t need to worry about it.

**Diagram**

```
Create → Inject → Init → Use → Destroy
```

**One-line recall:**

> Spring manages bean creation, initialization, usage, and destruction.

---

## J. Dependency Injection (DI)

DI = giving dependencies **from outside**, not letting the class create them.

* Makes code **loosely coupled**
* Easier to **test** and **maintain**
* Spring supports **constructor**, **setter**, and **autowiring**

**Diagram**

```
Car needs Engine
Spring injects Engine
```

**One-line recall:**

> DI = Spring provides required objects instead of me creating them.

---

## K. Constructor Injection

* Dependencies provided **during object creation** via constructor
* Best for **mandatory dependencies**

**Diagram**

```
new Car(Engine)
```

**One-line recall:**

> Constructor injection ensures object is fully ready when created.

---

## L. Setter Injection

* Dependencies provided **after object creation** via setter methods
* Good for **optional dependencies**
* Risk: object may be partially initialized if dependency is not set

**Diagram**

```
Car created
   |
setEngine()
```

**One-line recall:**

> Setter injection injects dependencies after object creation, optional but flexible.

---

## M. Challenge: Inversion of Control (IoC)

* Earlier: **I create objects**
* Now: **Spring creates objects**
* That shift = **IoC**

**Diagram**

```
Before: Me → Object
Now:    Spring → Object
```

**One-line recall:**

> IoC = control shifts from me to Spring.

---

## N. Introduction to Autowiring & Types

Autowiring = Spring **figures out dependencies automatically**, no XML property wiring required.

Types:

1. **By Name** – match variable name with bean ID
2. **By Type** – match class type (one bean only)
3. **By Constructor** – match constructor parameters

**Diagram**

```
Car depends on Specification
Spring finds matching bean automatically
```

**One-line recall:**

> Autowiring = Spring injects dependencies automatically.

---

## O. Autowiring by Name

* Spring matches **variable name** with **bean ID**
* Uses **setter method**
* If names don’t match → dependency is `null`
* Only **one bean per name**

**Diagram**

```
Car.specification
Bean id = specification ✅
Injected via setter
```

**One-line recall:**

> By name → variable name must match bean ID, setter used.

---

## P. Autowiring by Type

* Spring matches **class type**
* Only **one bean per type** allowed
* Uses setter method

**Diagram**

```
Car needs Specification
Spring finds 1 Specification bean ✅
```

**One-line recall:**

> By type → match class type; only one bean allowed.

---

## Q. Autowiring by Constructor

* Spring matches **constructor parameters**
* Injects dependency during **object creation**
* Setter not needed
* Only **one matching bean per type**

**Diagram**

```
Car(Specification)
Spring injects during creation ✅
```

**One-line recall:**

> By constructor → injects via constructor parameters when creating object.

---

# 🧠 FINAL ONE-LINE RECALL FOR ENTIRE SECTION

> **Spring manages object creation, dependencies, and lifecycle via IoC, DI, beans, and autowiring, enabling loosely coupled, flexible, and testable applications.**
