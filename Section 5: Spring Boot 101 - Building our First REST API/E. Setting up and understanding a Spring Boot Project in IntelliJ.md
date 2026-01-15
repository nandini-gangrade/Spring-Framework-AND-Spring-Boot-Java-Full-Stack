## Setting up & Understanding a Spring Boot Project in IntelliJ

*(Strong Recall Notes)*

---

## Step 1️⃣: After downloading from Spring Initializr

* I have a **ZIP file**
* I **extract (unzip)** it
* A folder is created
  → folder name = **project name** (e.g. `FirstSpring`)

This folder contains the **entire Spring Boot project**

---

## Step 2️⃣: Opening project in IntelliJ

* Open **IntelliJ**
* On welcome screen → click **Open**
* Select the extracted project folder
* Click **OK**

### Trust Project popup

* IntelliJ asks: *Do you trust this project?*
* Reason:

  * IntelliJ will run code from this folder
* Action:

  * Click **Trust Project**

Now IntelliJ loads the project 🎉

---

## Step 3️⃣: What IntelliJ does in background (important)

At the bottom, I see:

```
Updating Maven dependencies
```

Meaning:

* IntelliJ is downloading all libraries
* Libraries are based on `pom.xml`
* This happens automatically

👉 I don’t need to download anything manually

---

## Step 4️⃣: Understanding Project Structure (VERY IMPORTANT)

### Left side = Project Explorer

Main folders:

```
FirstSpring
 ├── src
 │   ├── main
 │   │   ├── java
 │   │   └── resources
 │   └── test
 ├── pom.xml
 └── External Libraries
```

---

## src/main/java (Java source code)

* This is where **all Java code lives**
* Package name is same as what I entered in Spring Initializr

Example:

```
com.embarkx.firstspring
```

Inside this package:

* One main class exists by default
  → `FirstSpringApplication.java`

This is the **starting point** of the app

---

## src/main/resources (non-Java files)

Contains:

* `static` → CSS, JS, images
* `templates` → HTML (Thymeleaf)
* `application.properties` → configuration

Memory tip:

> Java code → `java`
> Config + UI → `resources`

---

## src/test (Testing)

* All **test cases** go here
* Used for unit testing & integration testing

---

## pom.xml (MOST IMPORTANT FILE)

* Maven configuration file
* Written in XML
* Controls:

  * Project info
  * Java version
  * Dependencies

Inside pom.xml I see:

* Group ID
* Artifact ID
* Project name
* Java version
* Dependencies

Example dependency:

```
spring-boot-starter-web
```

Meaning:

* Web support
* REST APIs
* Embedded Tomcat
* MVC setup

👉 One dependency = many configurations

---

## External Libraries folder

* Auto-generated
* Contains:

  * Spring libraries
  * Tomcat
  * Jackson
  * Logging libs
* All downloaded via Maven

I **never edit this folder**

---

## Understanding the main class

### `FirstSpringApplication.java`

This class has:

```
@SpringBootApplication
```

This annotation means:

> “This is a Spring Boot application”

---

## What is @SpringBootApplication actually doing?

If I open it (Ctrl + Click), I see:

```
@Configuration
@EnableAutoConfiguration
@ComponentScan
```

### Meaning (very important)

* `@Configuration`

  * This class provides configuration

* `@EnableAutoConfiguration`

  * Spring Boot auto-configures things
  * Based on dependencies

* `@ComponentScan`

  * Scans packages for components
  * Controllers, Services, Repositories

So:

```
@SpringBootApplication
= 3 annotations combined
```

---

## Visual: Spring Boot Startup Flow

```
main()
  ↓
@SpringBootApplication
  ↓
Auto Configuration
  ↓
Component Scan
  ↓
Embedded Server Starts
```

---

## Spring Boot Parent (pom.xml)

At top of pom.xml:

```
spring-boot-starter-parent
```

Purpose:

* Provides default configuration
* Manages dependency versions
* Reduces manual setup

Memory:

> Parent = default rules + versions

---

## Big Picture Understanding

Spring Initializr:

* Creates project

IntelliJ:

* Imports project
* Downloads dependencies

Spring Boot:

* Auto-configures everything
* Runs with embedded server

---

## 🧠 One-Line Strong Recall

> **A Spring Boot project in IntelliJ consists of Java code, resources, pom.xml, and a main class annotated with @SpringBootApplication that auto-configures and runs the app using an embedded server.**
