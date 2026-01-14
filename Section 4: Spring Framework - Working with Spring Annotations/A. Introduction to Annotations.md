

# 🖊️ Section 4: Spring Framework – Working with Spring Annotations

---

## A. Introduction to Annotations

Okay, so annotations are **NOT actual logic**.
They don’t execute code.
They are just **extra information about my code**.

In simple words:

> Annotation = metadata = “info about the code”

I write normal Java code (classes, methods, variables).
Then I add annotations to **describe how this code should be treated** by:

* Compiler
* Frameworks (like Spring)
* Runtime environment

So annotations **guide behavior**, they don’t perform behavior.

---

### Why annotations exist (important thought)

Earlier:

* Everything was configured using **XML**
* Too much boilerplate
* Hard to maintain

Annotations were introduced in **Java 5**, and now they are everywhere because:

* Configuration is closer to code
* Less XML
* More readable and maintainable

---

### Simple mental model

```
My Java Code
   +
Annotations (metadata)
   ↓
Spring / Compiler / Runtime understands
how to treat my code
```

---

### Example I already know: `@Override`

This is the best example to understand annotations.

```
@Override
public void display() {
    ...
}
```

What is happening here?

* `@Override` does NOT override the method
* It just **tells the compiler**:
  👉 “Hey, this method already exists in parent class”

If I mess up the method signature:

* Compiler throws error immediately
* That’s annotation helping me

So again:

> Annotation = information, not implementation

---

### Very important clarification (exam + interview point)

❌ Annotation does NOT do work
✅ Framework reads annotation and does the work

Spring sees annotations and **acts accordingly**.

---

### Annotations in Spring (big picture)

Spring uses annotations to:

* Create beans
* Inject dependencies
* Define application layers
* Handle web requests
* Reduce XML configuration

So instead of writing:

```
<bean id="car" class="Car"/>
```

I can just write:

```
@Component
public class Car {
}
```

Spring understands it automatically.

---

### Common Spring Annotations (high-level understanding)

I don’t need to memorize behavior yet, just **what they represent**:

#### `@Component`

* Marks a class as a **Spring-managed bean**
* Generic component

#### `@Autowired`

* Tells Spring to **inject dependency automatically**

#### `@Qualifier`

* Used when **multiple beans of same type exist**
* Helps Spring choose the correct one

#### `@Value`

* Injects property values into beans

#### `@Repository`

* Used for **data access layer**
* Specialized version of `@Component`

#### `@Service`

* Used for **business logic layer**
* Also a specialized `@Component`

#### `@Controller`

* Used in web applications
* Handles HTTP requests

#### `@RequestMapping`

* Maps URLs to controller methods

#### `@SpringBootApplication`

* Entry point for Spring Boot apps
* Combination of multiple annotations

---

### Layered architecture (mental map)

```
Controller  → handles requests
Service     → business logic
Repository  → database operations
```

Each layer has its own annotation.

---

### Why annotations matter in Spring (self-note)

* Less XML
* Cleaner code
* Configuration + logic together
* Industry standard
* Almost every Spring project uses annotations heavily

---

## 🧠 One-Line Recall (Video A)

> **Annotations are metadata added to Java code that guide Spring, compiler, and runtime behavior without executing logic themselves.**

---

