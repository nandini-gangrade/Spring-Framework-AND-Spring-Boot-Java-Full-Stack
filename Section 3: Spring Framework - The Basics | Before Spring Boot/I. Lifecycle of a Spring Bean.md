# Lifecycle of a Spring Bean

---

## What is a Bean?

In Spring (and many frameworks), **objects that are managed by the framework are called *Beans***.

So instead of you creating objects using `new`, the framework:

* creates them
* configures them
* manages their lifecycle

Those managed objects are **beans**.

---

## Bean Definition

To work with beans, Spring needs something called a **bean definition**.

A **bean definition** includes all the configuration metadata that the Spring container needs to:

* create the bean
* configure the bean
* manage the bean throughout its lifecycle

In short:

> Bean definition = instructions for Spring about how to create and manage an object.

---

## Bean Configuration

Bean definitions can be provided in **multiple ways**.

### 1. XML Configuration

Beans can be configured using XML files.

* Each bean is defined using the `<bean>` tag
* Attributes specify:

  * class
  * properties
  * dependencies

Example idea (conceptual):

```
<bean id="myBean" class="com.example.MyBean">
    <property name="message" value="Hello"/>
</bean>
```

---

### 2. Annotation-based Configuration

Beans can also be configured using annotations such as:

* `@Component`
* `@Service`
* `@Repository`

Spring scans the classpath, finds these annotations, and automatically manages those classes as beans.

---

### 3. Java-based Configuration

Beans can also be defined using Java configuration classes instead of XML.

---

## Lifecycle of a Bean

Now let’s talk about the **actual lifecycle** — what happens to a bean from start to end.

---

### High-level lifecycle stages

From the slide:

```
Instantiation → Population of Properties → Initialization → Ready for use → Destruction
```

---

## Step-by-Step Bean Lifecycle

---

### 1. Instantiation

This is the **first phase**.

* Spring creates the bean instance
* Uses:

  * the bean definition
  * the constructor (default or parameterized)

At this stage:

* object exists
* properties are NOT set yet

---

### Diagram: Instantiation

```
Bean Definition
       |
       |
Spring Container
       |
Creates Bean Object
```

---

### 2. Population of Properties

After the object is created, Spring moves to **property population**.

* Bean properties are set
* Happens using:

  * setter injection
  * constructor injection
  * field injection

This is where **Dependency Injection** happens.

---

### Diagram: Property Population

```
Bean Object Created
       |
       |
Spring Container
       |
Injects Dependencies
Sets Properties
```

---

### 3. Initialization

Once all properties are set, Spring performs **initialization**.

* Initialization methods are invoked
* Bean is prepared for use

This step happens **after dependency injection**.

---

### 4. Ready for Use

After initialization:

* Bean is fully configured
* Bean is ready to be used by the application
* Can be requested from the Spring container at any time

---

### Diagram: Bean Ready State

```
Initialized Bean
       |
       |
Spring Container
       |
Provides Bean to Application
```

---

### 5. Destruction

This is the **final phase**.

* Happens during application shutdown
* Bean is removed from the container
* Cleanup logic is executed

Once destroyed:

* Bean no longer exists in the container

---

### Diagram: Destruction Phase

```
Application Shutdown
       |
       |
Spring Container
       |
Destroys Bean
Releases Resources
```

---

## Dependency Resolution in Lifecycle

During the lifecycle, Spring also handles **dependency resolution**.

This includes:

* Dependency Injection
* Autowiring

Spring ensures that:

* required dependencies are identified
* correct objects are injected at the right time

---

## Complete Lifecycle Flow (One View)

```
Bean Definition
       |
Instantiation
       |
Property Population
       |
Initialization
       |
Ready for Use
       |
Destruction
```

---

## Key Takeaways

* Beans are objects managed by Spring
* Bean definition tells Spring how to create and manage beans
* Beans can be configured using:

  * XML
  * Annotations
  * Java configuration
* Bean lifecycle has clear stages:

  * Instantiation
  * Property population
  * Initialization
  * Ready for use
  * Destruction
* Dependency Injection happens during property population

---

## One-line summary

> **Spring controls the complete lifecycle of a bean — from creation, dependency injection, usage, all the way to destruction.**

---

That’s the **Bean Lifecycle** done clean and complete.
Next section will feel much easier now because this concept sits underneath almost everything in Spring.
