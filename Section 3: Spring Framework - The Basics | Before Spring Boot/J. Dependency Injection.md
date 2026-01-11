# Dependency Injection (DI)

---

## What is Dependency Injection?

**Dependency Injection (DI)** is a design pattern used in software development to achieve **loose coupling** between classes.

The main idea is simple:

> Instead of a class creating its own dependencies, those dependencies are provided to it from the outside.

---

## Why Dependency Injection?

Normally, in object-oriented programming, one class creates another class directly.

That means:

* One class knows **exactly how** another class is created
* Classes become tightly coupled
* Changing one dependency often forces changes in multiple places

Dependency Injection solves this by:

* Removing direct dependency instantiation from the dependent class
* Providing dependencies **on the fly at runtime**

This helps achieve **loose coupling**.

---

## Without Dependency Injection (Tight Coupling)

Conceptually, this is what usually happens without DI:

```
Class A
   |
   | creates
   v
Class B
```

* Class A directly instantiates Class B
* Class A is tightly coupled to Class B
* Changing Class B affects Class A

---

## With Dependency Injection (Loose Coupling)

With DI, the flow changes:

```
Spring Container
       |
       |
Provides Dependency
       |
       v
Class A  ----> uses ----> Interface
```

* Class A does not create the dependency
* Dependency is provided during runtime
* Class A depends on an abstraction, not an implementation

---

## How Dependency Injection Works

The dependency:

* is **not instantiated inside the class**
* is **injected from outside**
* is usually injected by a framework like Spring

Spring performs this injection at runtime using the configuration provided by the developer.

---

## Types of Dependency Injection

There are **two main types** of dependency injection:

```
Dependency Injection
        |
        |
  -----------------
  |               |
Constructor    Setter
Injection      Injection
```

---

## 1. Constructor Injection

In **constructor injection**:

* Dependencies are provided through the constructor
* The object cannot be created without its dependencies

Key points:

* Dependency is mandatory
* Object is always in a valid state
* Injection happens at object creation time

Conceptual flow:

```
Spring Container
       |
Calls Constructor
       |
Passes Dependency
       |
Creates Object
```

---

## 2. Setter Injection

In **setter injection**:

* Dependencies are provided using setter methods
* Object is created first
* Dependencies are injected later

Key points:

* Dependency is optional
* More flexible
* Injection happens after object creation

Conceptual flow:

```
Spring Container
       |
Creates Object
       |
Calls Setter
       |
Injects Dependency
```

---

## Constructor vs Setter Injection (Quick Comparison)

| Feature                | Constructor Injection  | Setter Injection             |
| ---------------------- | ---------------------- | ---------------------------- |
| When injection happens | During object creation | After object creation        |
| Dependency required    | Yes                    | Optional                     |
| Object state           | Always complete        | May be partially initialized |
| Flexibility            | Less                   | More                         |

---

## Why Dependency Injection Matters in Spring

Dependency Injection is a **core concept** in Spring.

Spring:

* Creates objects
* Resolves dependencies
* Injects dependencies automatically
* Manages the entire lifecycle

Because of DI:

* Classes stay loosely coupled
* Code becomes easier to test
* Implementations can be swapped without changing dependent code

---

## Key Takeaways

* Dependency Injection is a design pattern
* It helps achieve loose coupling
* Dependencies are provided externally, not created internally
* Spring handles dependency injection at runtime
* Two main types exist:

  * Constructor Injection
  * Setter Injection

---

## One-line Summary

> **Dependency Injection removes the responsibility of creating dependencies from a class and hands it over to the container.**

---

Next step is seeing **constructor injection and setter injection in real Spring code**, which will make this feel very natural.
