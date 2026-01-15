

## 🧠 @Autowired Annotation (Strong Recall Notes)

---

## What this video is about (talking to myself)

> “Now I’m learning how Spring automatically puts one object inside another object without me writing `new` keyword.”

This is called **automatic dependency injection** using `@Autowired`.

---

## First, why do we even need @Autowired?

Earlier, without Spring, I used to do this:

```
Employee emp = new Employee();
Manager mgr = new Manager(emp);
```

Problems with this:

* I am creating objects myself
* Classes are tightly coupled
* Spring container is not fully used

Spring idea is:

> “You don’t create objects. I (Spring) will create and inject them.”

And **@Autowired** is the instruction for that.

---

## What is @Autowired? (simple words)

`@Autowired` is an annotation that tells Spring:

> “Spring, please automatically inject the required dependency here.”

* Dependency = another object this class needs
* Inject = put that object inside automatically

No `new` keyword.
No manual wiring.

---

## Project setup (what I did)

I copied existing classes:

* `App`
* `AppConfig`
* `Employee`

And pasted them into a new package:

```
com.example.autowired.annotation
```

(Important: different from autowire-by-name/type packages)

---

## Step 1: Create a dependency example

I created a new class:

```
Manager.java
```

Inside `Manager`, I added:

```
private Employee employee;
```

Meaning:

> “Manager depends on Employee”

This is **dependency relationship**.

---

## Step 2: Register Manager as Spring Bean

I added:

```
@Component
```

Above `Manager` class.

Why?

* So Spring can manage `Manager`
* So Spring can inject dependencies into it

No `@Component` ❌ → Spring won’t know this class exists.

---

## Step 3: Constructor Injection using @Autowired

I created a constructor:

```
public Manager(Employee employee) {
    this.employee = employee;
}
```

Then added:

```
@Autowired
```

Above constructor.

Meaning I’m telling Spring:

> “When creating Manager, please provide Employee automatically.”

Spring behavior:

1. Looks at Manager
2. Sees it needs Employee
3. Finds Employee bean
4. Injects it automatically

💡 This is **constructor injection**.

---

## Diagram – Constructor Injection

```
Spring Container
      |
      |-- Employee bean
      |
      |-- Manager bean
            |
            |-- Employee injected via constructor
```

---

## Step 4: Test it from App class

In `App.java`:

```
Manager manager = context.getBean("manager", Manager.class);
System.out.println(manager);
```

Output showed:

* Manager object
* Inside it → Employee object (not null)

So injection worked 🎉

---

## Important Question: Is constructor mandatory?

I asked myself:

> “Do I always need constructor for @Autowired?”

Answer: ❌ NO

Let’s see what happens.

---

## Step 5: Remove constructor (test)

I commented out the constructor.

Result:

* `employee` became **null**
* Because Spring had no instruction how to inject

So constructor injection is required **if @Autowired is on constructor**.

---

## Step 6: Field Injection using @Autowired

Instead of constructor, I wrote:

```
@Autowired
private Employee employee;
```

This is called **field injection**.

Now Spring:

* Directly injects Employee into the field
* No constructor needed

Result:
✅ Employee injected again

---

## Diagram – Field Injection

```
Manager
  |
  |-- @Autowired Employee (directly injected)
```

---

## Types of Injection learned here

### 1️⃣ Constructor Injection (Recommended ✅)

```
@Autowired
public Manager(Employee employee) { }
```

✔ Clear dependencies
✔ Best practice
✔ Easier testing

---

### 2️⃣ Field Injection (Works but not preferred)

```
@Autowired
private Employee employee;
```

✔ Less code
✔ Cleaner class
❌ Hidden dependencies
❌ Harder to test

---

## Which one should I use? (Interview + real world)

Best practice:

> **Constructor Injection is preferred over Field Injection**

Why?

* Makes dependencies obvious
* Safer
* More maintainable

---

## What @Autowired actually does (inside Spring)

When Spring sees `@Autowired`:

1. It checks required type
2. Finds matching bean
3. Injects it automatically
4. Throws error if no matching bean found

So Spring IoC container is doing all the work.

---

## Talking to myself (final clarity)

> “@Autowired saves me from writing wiring code. Spring finds the dependency and injects it automatically, either via constructor or directly into field.”

---

## 🧠 One-Line Recall (VERY IMPORTANT)

> **@Autowired tells Spring to automatically inject required dependencies into a bean, preferably using constructor injection.**
