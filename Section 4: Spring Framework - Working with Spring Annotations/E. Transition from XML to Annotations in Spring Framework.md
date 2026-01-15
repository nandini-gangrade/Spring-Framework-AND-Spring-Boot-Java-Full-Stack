## 5️⃣ Transition from XML to Annotations (Complete shift)

---

## What this video is about (in my own words)

Till now, I was using **XML** to tell Spring:

* where to scan components
* how to configure beans

But modern Spring prefers **annotations**.

So in this video, I learned:

> **How to completely remove XML and use only annotations for configuration**

---

## What we were doing earlier (XML way)

Earlier we had an XML file like:

```
component-scan-demo.xml
```

Inside it, we wrote:

```
<context:component-scan base-package="com.example.component.scan" />
```

Meaning:

> “Spring, please scan this package and find components.”

This works ✅
But we want to **remove XML** now.

---

## New approach (Annotation-based config)

Instead of XML file ➜ we create a **Java class**.

This class will act like:

> “replacement of XML file”

---

## Step 1: Create a configuration class

I created a new package:

```
com.example.component.scan.annotation
```

Inside it, I created a class:

```
AppConfig
```

Important understanding:

* This class is NOT for logic
* It is ONLY for configuration

(No methods, no fields needed)

---

## Step 2: Tell Spring this is a config class

For that, I used:

```
@Configuration
```

Meaning:

> “Hey Spring, this class contains configuration.”

So Spring treats it like:
📄 XML file replacement

---

## Step 3: Tell Spring where to scan components

Earlier we did this in XML.

Now we do it using annotation:

```
@ComponentScan(basePackages = "com.example.component.scan.annotation")
```

Meaning:

> “Spring, scan this package and all its sub-packages for @Component classes.”

So now **component scanning is fully annotation-based**.

---

## AppConfig summary (in mind)

```
@Configuration
@ComponentScan(basePackages = "com.example.component.scan.annotation")
public class AppConfig {
    // no code needed
}
```

This single class replaces:
❌ XML file
❌ context:component-scan

---

## Step 4: Change ApplicationContext type

Earlier we wrote:

```
ApplicationContext context =
    new ClassPathXmlApplicationContext("component-scan-demo.xml");
```

This loads **XML-based configuration**.

But now we are using annotations.

So we change it to:

```
ApplicationContext context =
    new AnnotationConfigApplicationContext(AppConfig.class);
```

Meaning:

> “Spring, load configuration from AppConfig class.”

Very important change 🔥

---

## Common mistake & debugging lesson

Error came:

```
No bean named 'employee' available
```

Why?

👉 Typo in package name inside `@ComponentScan`

Mistake example:

```
car.example...
```

Correct:

```
com.example...
```

Lesson I learned:

* If bean not found → always check:

  * package names
  * spelling
  * component scan path

Best practice:
📋 Copy package name instead of typing

---

## Final result (what we achieved)

✔ No XML file
✔ Only annotations
✔ Spring loads config from Java class
✔ Components auto-detected
✔ Application runs successfully

We **completely eliminated XML**.

---

## Diagram – XML vs Annotation

### Before (XML way)

```
XML File
   |
   |-- component-scan
   |-- bean definitions
```

### Now (Annotation way)

```
AppConfig.java
   |
   |-- @Configuration
   |-- @ComponentScan
```

---

## Why this is important (real world)

* Cleaner code
* Less files
* Easier maintenance
* Industry standard
* Used heavily in Spring Boot

Spring Boot is basically:

> **Annotation-based configuration on steroids**

---

## Talking to myself (final understanding)

> “Earlier XML told Spring what to do. Now annotations + config class do the same job, but cleaner and modern.”

---

## 🧠 One-Line Recall

> **We replace XML with a @Configuration class and use AnnotationConfigApplicationContext to load annotation-based Spring configuration.**
