# 🖊️ Section 4: Spring Framework – Working with Spring Annotations

## B. Understanding Components and ComponentScan

---

## 1️⃣ What is a Component? 

Okay, first thing:
**Component is NOT something new or different from a bean.**

A **component is a bean**, but with one important idea:

> A component is a bean that Spring can **auto-detect**.

So:

* Bean → managed by Spring IOC container
* Component → also managed by Spring IOC container
* Difference → *how it is discovered*

Earlier, I was **manually defining beans** in XML.
Now, with components, **Spring finds them on its own**.

---

### Simple definition I should remember

> **A component is a Java class managed by Spring’s IoC container and auto-detected using classpath scanning.**

---

## 2️⃣ Where do components live?

Components are:

* Building blocks of a Spring application
* Each component provides **some functionality**

  * business logic
  * data access
  * services
  * controllers (later)

---

## 3️⃣ Component vs Bean (important clarity)

This confusion is very common, so let me explain it to *myself* clearly.

### Bean (traditional way)

* Defined explicitly
* Usually via XML or Java config

```
<bean id="car" class="Car"/>
```

### Component (annotation way)

* Discovered automatically
* No need to define each bean manually

```
@Component
public class Car {
}
```

👉 **Internally both are beans**
👉 Difference is **manual vs automatic registration**

---

### Mental shortcut (exam / interview)

```
Component ⊂ Bean
```

Every component is a bean,
but not every bean is a component.

---

## 4️⃣ How do I create a Component?

There are **two ways**:

---

### ✔️ Way 1: XML (old / manual)

This is what I already know:

```
<bean id="myBean" class="com.example.MyClass"/>
```

But this does NOT auto-detect anything.

---

### ✔️ Way 2: Annotations (modern / preferred)

I simply add:

```
@Component
public class MyClass {
}
```

That’s it.

Now Spring **knows**:

* This class should be managed
* This class should become a bean

📌 Important:
`@Component` comes from
`org.springframework.stereotype`

---

## 5️⃣ So what is Component Scanning?

Now comes the **most important missing link**.

I told Spring:

> “This class is a component”

But Spring now asks:

> “Okay… but **where should I look** for components?”

That’s where **ComponentScan** comes in.

---

### ComponentScan = telling Spring where to look

> Component scanning is a feature that tells Spring **which packages to scan** to find components.

Spring does NOT scan the entire project by default.
I must **explicitly tell it**.

---

## 6️⃣ How Component Scanning works (step-by-step)

Let me explain this to myself slowly.

### Step 1: I create components

```
@Component
public class Car { }
```

```
@Component
public class Engine { }
```

### Step 2: I tell Spring where to scan

```
<context:component-scan base-package="com.example.app"/>
```

### Step 3: Spring does this internally

* Goes to `com.example.app`
* Scans all classes
* Also scans **sub-packages**
* Finds `@Component`
* Registers them as beans

---

## 7️⃣ Diagram (very important for recall)

```
Spring IOC Container
        |
        |-- scans --> com.example.app
                       |
                       |-- Car (@Component)
                       |-- Engine (@Component)
                       |-- Service (@Component)
                       |-- sub-packages also scanned
```

Everything found becomes a **Spring bean automatically**.

---

## 8️⃣ Key rules I must remember

* Component scanning:

  * Works on **packages**
  * Includes **sub-packages**
* If package is NOT scanned:

  * Component exists
  * But Spring will **ignore it**
* Component ≠ magically loaded
  👉 Scanning must be enabled

---

## 9️⃣ Why this is powerful (self reflection)

Before:

* Too much XML
* Manual wiring
* Error-prone

Now:

* Just annotate classes
* Tell Spring where to scan
* Spring manages everything

This is the **base of annotation-driven Spring**.

---

## 🧠 One-Line Recall (Video B)

> **A component is a Spring-managed bean that is auto-detected via component scanning, which tells Spring which packages to scan and register as beans.*
