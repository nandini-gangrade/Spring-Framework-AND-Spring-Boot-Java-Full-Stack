
## Getting Started with Spring Initializr (Strong Recall Notes)

---

## What is Spring Initializr?

* Spring Initializr is a **project generation tool**
* Website: **start.spring.io**
* Purpose:
  → Create a ready-to-run Spring Boot project in seconds
* Especially useful if:

  * Using **IntelliJ Community Edition**
  * No built-in Spring Boot project wizard

👉 Bookmark this site. You’ll use it a lot.

---

## Why Spring Initializr exists (problem it solves)

Without Initializr:

* Manual project setup
* Manual dependency management
* High chance of config mistakes

With Initializr:

* Pre-built project structure
* Correct dependencies
* Ready to import and run

Think:

> “Project skeleton + configuration done for me”

---

## Step 1️⃣: Choosing Project Type

```
Project: Maven
Language: Java
```

Why Maven:

* Most common
* Dependency management is simple
* Industry standard

(Gradle is optional, not wrong)

---

## Step 2️⃣: Spring Boot Version

Key rule:

* ❌ Avoid **SNAPSHOT** versions
* ✅ Use **stable release**

Why avoid snapshot:

* Pre-release
* May contain bugs
* Not production-ready

Important note:

* Version numbers may change
* Always select **latest stable**
* Prefer **Spring Boot 3.x**

Memory hook:

> Snapshot = experimental, Stable = safe

---

## Step 3️⃣: Project Metadata

### Group

* Represents **base package**
* Usually reverse domain name

Example:

```
com.embarkx
```

### Artifact

* Project name
* Also becomes:

  * Folder name
  * Jar name

Example:

```
first-spring
```

### Description

* Human-readable project description
* No technical impact

### Final package structure auto-created

```
com.embarkx.firstspring
```

Spring Initializr auto-generates this.

---

## Step 4️⃣: Packaging & Java Version

### Packaging

```
Jar ✅
War ❌ (unless deploying to external server)
```

Jar:

* Executable
* Best for Spring Boot
* Embedded server support

### Java Version

```
Java 17
```

Why Java 17:

* LTS (Long Term Support)
* Recommended for Spring Boot 3

---

## Step 5️⃣: Dependencies (MOST IMPORTANT)

Dependencies = **features**

Click **Add Dependencies**

### For Web Application

Select:

```
Spring Web
```

What Spring Web gives:

* Spring MVC
* REST support
* Embedded Tomcat
* HTTP handling

One dependency → many configurations auto-added

---

## Dependency Categories (mental map)

```
Web            → REST, MVC, Tomcat
Dev Tools      → Auto-restart, live reload
Template       → Thymeleaf
Security       → Auth, authorization
SQL            → JDBC, MySQL, PostgreSQL
NoSQL          → MongoDB, Redis
```

Key idea:

> You don’t configure features, you select dependencies

---

## Step 6️⃣: Explore Project (optional but useful)

Click **Explore**

Shows:

* pom.xml
* src/main/java
* src/main/resources
* application.properties

This answers:

> “What will be created if I download?”

---

## Step 7️⃣: Generate Project

* Click **Generate**
* ZIP file downloads
* Extract it
* Import into IntelliJ

Project is now:

* Runnable
* Pre-configured
* Server-ready

---

## Visual: What Spring Initializr Actually Does

```
Your choices
   ↓
Spring Initializr
   ↓
Pre-configured project
   ↓
Import → Run → Build
```

---

## Key mindset shift

Old way:

* Setup first
* Code later

Spring Boot way:

* Generate
* Code immediately

---

## 🧠 One-Line Strong Recall

> **Spring Initializr generates a fully configured Spring Boot project by selecting project type, version, metadata, and dependencies—ready to run instantly.**

