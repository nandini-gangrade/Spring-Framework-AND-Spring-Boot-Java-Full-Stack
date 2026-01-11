# Setting Up a Spring Project (Using Maven)

---

## Why this step is needed

To use Spring features in a Java application, the project must first be converted into a **Spring-enabled project**.
This is done by adding the required **Spring dependencies** using **Maven**.

Without these dependencies, Spring concepts like:

* IoC
* Dependency Injection
* Beans
* Spring Container

cannot be used.

---

## Project setup overview

The project is already created as a **Maven project**.

That means:

* It contains a special file called **pom.xml**
* This file controls:

  * project configuration
  * Java version
  * dependencies (external libraries)

---

## Understanding `pom.xml`

### What `pom.xml` is

`pom.xml` is the configuration file for Maven.

It contains:

* project details
* Java compiler version
* list of dependencies needed by the project

---

### Java version configuration

In the project, Java version **21** is already defined.

This means:

* source code is compiled using Java 21
* target bytecode is Java 21

This was selected during project creation.

---

## Goal: Convert Maven project into Spring project

To convert this project into a Spring project, **Spring dependencies** must be added to `pom.xml`.

Maven will then:

* download required JAR files
* manage them automatically

---

## Why Maven is important here

Before Maven existed:

* developers manually downloaded `.jar` files
* copied them into the project
* configured them manually

This was:

* time-consuming
* error-prone
* difficult to manage

With Maven:

* dependencies are declared once
* Maven downloads correct versions automatically
* related dependencies are resolved automatically

---

## Maven Repository

### What it is

Maven Repository is an online repository that contains:

* all popular Java libraries
* their versions
* dependency details

It allows developers to:

* search
* browse
* copy dependency definitions

---

## Spring dependencies required

To enable Spring features, **two dependencies** are required:

1. **Spring Core**
2. **Spring Context**

---

## Dependency 1: Spring Core

### What Spring Core is

Spring Core is the **foundation of the Spring Framework**.

It provides:

* core utilities
* dependency injection
* inversion of control support
* basic building blocks required by Spring

Spring Core works together with Spring Beans to enable IoC and DI.

---

### Adding Spring Core dependency

Steps:

1. Search for **Spring Core** in Maven Repository
2. Select the **latest version**
3. Copy the Maven dependency snippet
4. Add it inside `<dependencies>` tag in `pom.xml`

---

### Important note about versions

Spring releases new versions frequently.

If a newer version is available:

* selecting the latest stable version is fine
* steps remain the same

---

## Dependency 2: Spring Context

### What Spring Context is

Spring Context builds on top of Spring Core.

It provides:

* ApplicationContext
* bean lifecycle management
* advanced container features

Spring Context is required to:

* work with Spring Container
* manage beans properly

---

### Adding Spring Context dependency

Steps:

1. Search for **Spring Context** in Maven Repository
2. Select the **latest version**
3. Copy the Maven dependency snippet
4. Paste it under the Spring Core dependency

---

## Final structure inside `pom.xml`

```
<dependencies>
    <dependency>
        spring-core
    </dependency>

    <dependency>
        spring-context
    </dependency>
</dependencies>
```

Red marks may appear temporarily — this is normal.

---

## Reloading Maven changes

After modifying `pom.xml`, Maven must be reloaded.

Why?

* Maven needs to download new dependencies
* external libraries must be updated

---

### How to reload

Two ways:

1. Click **Refresh** icon in the IDE
2. Use the **Maven panel (M icon)** and refresh

---

## What happens after refresh

Maven will:

* download Spring Core
* download Spring Context
* download all related dependencies automatically

These appear under **External Libraries**.

---

### Diagram: Dependency resolution

```
pom.xml
   |
   |-- spring-core
   |-- spring-context
   |
Maven
   |
   |-- downloads jars
   |-- resolves related dependencies
   |
External Libraries
```

Even though only two dependencies were added, many JAR files appear.
These are **transitive dependencies** required by Spring.

---

## Result after setup

* Project is now Spring-enabled
* Spring Core features are available
* Spring Context (ApplicationContext) is available
* Ready to use:

  * IoC
  * Dependency Injection
  * Beans
  * Spring Container

No manual JAR handling required.

---

## Key takeaway (one-line recall)

> **Adding Spring Core and Spring Context dependencies using Maven converts a Maven project into a Spring project and enables Spring features.**
