# Introduction to Autowiring and its Types

---

## Why do we even need Autowiring? 

Till now, what was I doing?

I was **explicitly telling Spring** about dependencies using XML.

Example:

* This bean **needs** that bean
* I was manually writing `<property>` or `<constructor-arg>`

So basically:

* Earlier: Java code managed dependencies
* Then: XML managed dependencies
* Now: **Spring itself can manage dependencies automatically**

So question I asked myself:

> If Spring already knows my classes and their variables,
> **why am I still manually wiring them?**

That’s where **Autowiring** comes in.

---

## What is Autowiring (simple meaning)

**Autowiring** means:

> Spring automatically finds and injects required dependencies **by itself**,
> without me explicitly defining `<property>` or `<constructor-arg>`.

In short:

* I don’t say *what depends on what*
* Spring looks at the code and **figures it out**

---

## Before Autowiring vs After Autowiring

### Before (what we were doing)

```
XML:
Car needs Specification
I explicitly write reference
```

Control is still **partly with me**.

### After Autowiring

```
Spring sees:
Car has Specification variable
Spring injects it automatically
```

Control moves **more towards Spring**.

---

## Simple real-life example (for my brain)

Think like this:

### Without Autowiring

I say:

> “Hey Spring, give this car *this exact engine*.”

### With Autowiring

Spring says:

> “I see this car needs an engine.
> I already have one. I’ll put it in.”

---

## Important requirement for Autowiring

For autowiring to work:

✔ There must be **at least two beans**
✔ One bean must **depend on another**

Example:

```
Car → depends on → Specification
```

If there is no dependency, autowiring makes no sense.

---

## Types of Autowiring (VERY IMPORTANT)

There are **3 types** we need to remember.

I’ll explain each **slowly and simply**.

---

## 1️⃣ Autowiring by Type

### What “type” means

Type = **class type**

Example:

```
Specification specification;
```

Type here is `Specification`.

### How Spring works

Spring says:

> “This variable is of type Specification.
> Let me find a bean of type Specification.”

If Spring finds **one matching bean**, it injects it.

### Diagram

```
Car
 |
 |-- Specification (type)
 |
Spring injects bean of same type
```

### Important note to myself

* If **more than one bean of same type exists** → ❌ error
* By-type needs **only one matching bean**

---

## 2️⃣ Autowiring by Name

### What “name” means

Name = **variable name**

Example:

```
Specification specification;
```

Variable name = `specification`

### How Spring works

Spring says:

> “Let me find a bean whose **ID name** matches this variable name.”

So if bean ID is:

```
id="specification"
```

Spring injects it.

### Diagram

```
Variable name: specification
Bean id:       specification
→ Match found → Inject
```

### Important note

* Bean ID **must match variable name exactly**
* Even spelling matters

---

## 3️⃣ Autowiring by Constructor

### What happens here

Spring looks at the **constructor parameters**.

Example:

```
Car(Specification specification)
```

Spring says:

> “This constructor needs Specification.
> I’ll inject it while creating the object.”

### Diagram

```
Spring creates Car
 |
 |-- Constructor needs Specification
 |
Spring injects Specification during creation
```

### Why this is powerful

* Dependency is available **at object creation time**
* Very safe and clean

---

## Summary of all 3 types (mental table)

```
By Type        → matches class type
By Name        → matches variable name with bean ID
By Constructor → matches constructor arguments
```

---

## Why Autowiring is useful (benefits)

✔ Less XML
✔ Less manual wiring
✔ Cleaner configuration
✔ Faster development
✔ Code speaks for itself

Spring reads the code and understands dependencies.

---

## Disadvantage (important to remember)

With XML:

* I had **full control**
* I decided exactly which bean goes where

With Autowiring:

* Spring decides
* I lose **some control**
* Debugging can be harder if many beans exist

So:

> Convenience ↑
> Control ↓

---

## How this connects to Spring Boot (preview)

In Spring Boot:

* Autowiring is used **everywhere**
* Mostly done using `@Autowired`
* XML is rarely used

So this concept is:

> **core foundation for Spring Boot**

---

## Key takeaways (me revising)

* Autowiring = automatic dependency injection
* Spring decides dependencies using rules
* Three types: by type, by name, by constructor
* Less config, more automation
* Slight loss of control

---

## One-line recall (final)

> **Autowiring means Spring automatically injects dependencies by understanding my code, not my XML.**
