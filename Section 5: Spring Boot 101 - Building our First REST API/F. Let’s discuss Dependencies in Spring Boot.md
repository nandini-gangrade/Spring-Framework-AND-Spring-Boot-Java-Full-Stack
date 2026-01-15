# 🖊️ Dependencies in Spring Boot


---

## What are dependencies?

* Dependencies = **external libraries** my app needs to work
* Example:

  * Web → Spring MVC, Tomcat
  * DB → JDBC, Hibernate
  * Dev tools → auto restart, logging

Without dependencies → app can’t run properly

---

## How Spring Boot manages dependencies

* Spring Boot uses:

  * **Maven** or
  * **Gradle**

In my project:

* I selected **Maven**
* So dependency file = **pom.xml**

---

## pom.xml (dependency manager)

* `pom.xml` controls:

  * What libraries are used
  * Which versions are used
  * How project is built

Structure reminder:

```xml
<dependencies>
    <dependency>
        ...
    </dependency>

    <dependency>
        ...
    </dependency>
</dependencies>
```

* Every library = one `<dependency>` block
* Maven downloads everything automatically

---

## Spring Boot Starter Dependencies (very important)

* Spring Boot gives **starter dependencies**
* Starter = **bundle of related libraries**

Example:

```
spring-boot-starter-web
```

This one dependency includes:

* Spring MVC
* Embedded Tomcat
* Jackson (JSON)
* Validation
* Logging

👉 I don’t add these one by one
👉 Starter does it for me

---

## Why starters are powerful

* Less boilerplate
* No version conflicts
* Faster setup
* Clean pom.xml

Memory line:

> One starter = many libraries pre-wired

---

## Adding non-spring dependencies

Apart from Spring starters, I can add:

* Database drivers
* Caching libraries
* Utility libraries
* Third-party frameworks

All go into **pom.xml**

---

## Maven Central Repository

Website:

```
search.maven.org
```

Purpose:

* Official repository for Java libraries
* Maintained by Maven community

What I can do here:

* Search any dependency
* Copy Maven snippet
* Choose version
* Paste into pom.xml

---

## Example: Adding Spring Boot DevTools

Steps:

1. Go to **search.maven.org**
2. Search → `spring-boot-devtools`
3. Click result
4. Copy Maven dependency snippet
5. Paste inside `<dependencies>` in pom.xml

That’s it.

---

## Dependency snippet example (mental model)

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
</dependency>
```

After saving:

* Maven auto-downloads
* IntelliJ refreshes project

---

## Choosing dependency versions

* Maven Central shows:

  * Latest version
  * Older versions
* I can pick specific version if needed

Rule of thumb:

* Prefer **stable versions**
* Avoid snapshot versions in production

---

## Spring Initializr vs Maven Central

### Spring Initializr

* Curated list
* Common Spring use cases
* Stable & safe
* Beginner-friendly

### Maven Central

* Everything exists here
* For:

  * Rare libraries
  * Niche tools
  * Advanced needs

---

## Why some dependencies are NOT in Spring Initializr

Reasons:

* Too new / experimental
* Not commonly used
* Niche or custom libraries
* Not yet community-approved

So:

> If not in Initializr → use Maven Central

---

## Visual: Dependency Flow

```
pom.xml
   ↓
Maven
   ↓
Downloads libraries
   ↓
External Libraries
   ↓
Spring Boot auto-configures
```

---

## Big Picture Understanding

* Dependencies define **what my app can do**
* Spring Boot starters reduce complexity
* pom.xml is the single source of truth
* Maven Central = backup for anything missing

---

## 🧠 One-Line Strong Recall

> **Dependencies in Spring Boot are managed via pom.xml using Maven, where starter dependencies bundle common libraries and Maven Central provides access to any additional external libraries needed.**

