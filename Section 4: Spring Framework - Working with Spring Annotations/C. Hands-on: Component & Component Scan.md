## C. Hands-on: Component & Component Scan (Without Annotations *earlier*, now using @Component)

---

## What this video was really about (in my own words)

This video is basically answering one question:

> **“If I stop defining beans in XML, how does Spring still know what to manage?”**

And the answer is:
👉 **Component + Component Scan**

---

## Step 1️⃣ Creating a normal Java class (Employee)

First, I created a **plain Java class**:

```
Employee
- employeeId
- firstName
- lastName
- salary
```

At this point:

* It’s just a POJO
* Spring knows NOTHING about it
* It’s not a bean yet

So right now:

```
Employee  --->  Just a normal Java object
```

---

## Step 2️⃣ Old way: Bean via XML (and why we commented it)

Earlier, I *could* do this:

```
<bean id="employee" class="com.example.componentScan.Employee"/>
```

This works, but:

* Manual
* Verbose
* Not scalable

So we **commented this out** on purpose to test something new.

---

## Step 3️⃣ Turning Employee into a Component

Now comes the key change:

```
@Component
public class Employee {
}
```

What this means (important):

> “Hey Spring, this class is important.
> Please manage it for me.”

⚠️ Very important realization:

* `@Component` **does not create the bean by itself**
* It only *marks* the class as eligible

At this point, Spring STILL doesn’t know about it unless we scan.

---

## Step 4️⃣ Creating ApplicationContext (App.java)

In `App.java`, I did:

```
ApplicationContext context =
    new ClassPathXmlApplicationContext("componentScanDemo.xml");
```

And then:

```
Employee emp = context.getBean(Employee.class);
```

At this moment, I expected it to work…

❌ **But it failed**

---

## Step 5️⃣ The Error (and why it happened)

Error:

> **No bean named 'employee' available**

This error is GOOD.
It tells me something important:

> “Spring did NOT find any bean called Employee”

Why?

Because:

* I marked the class with `@Component`
* BUT I never told Spring **where to look**

---

## Step 6️⃣ Component Scan (the missing piece)

This is the **core learning** of this video.

Spring needs instructions like:

> “Scan THIS package for components”

So in XML, we added:

```
<context:component-scan base-package="com.example.componentScan"/>
```

Also important:

* We had to add `context` namespace
* Otherwise XML won’t understand `component-scan`

---

## Step 7️⃣ What happens internally (very important)

After adding component scan, Spring does this:

```
1. Start Spring Container
2. Look at componentScanDemo.xml
3. See base-package = com.example.componentScan
4. Scan that package
5. Find @Component on Employee
6. Register Employee as a bean
```

So now:

```
Employee  --->  Spring Bean ✔
```

---

## Step 8️⃣ Diagram (mental picture)

```
Spring Container
      |
      |-- component-scan
             |
             |-- com.example.componentScan
                    |
                    |-- Employee (@Component) ✔
```

No XML bean definition needed anymore.

---

## Step 9️⃣ Bean Name – default vs custom

### Default behavior (VERY IMPORTANT)

If I write:

```
@Component
public class Employee { }
```

Spring registers bean as:

```
employee
```

Rule:

> **Class name with first letter lowercase**

---

### Custom bean name

If I write:

```
@Component("employeeOne")
```

Now Spring registers it as:

```
employeeOne
```

So:

* `getBean("employee")` ❌
* `getBean("employeeOne")` ✅

This explains why:

* Changing the name broke the code
* Matching name fixed it

---

## Step 🔟 Why values were null (and why it’s okay)

Output was something like:

```
employeeId = 0
firstName = null
salary = 0.0
```

Why?

* Spring created the object
* But we never set values yet
* No injection done so far

This is expected at this stage.

---

## Final Understanding (self-check)

* `@Component` → marks a class
* `component-scan` → activates detection
* Both are required
* Without scan → component is ignored
* Without component → scan finds nothing

---

## 🧠 One-Line Recall (Strong)

> **@Component marks a class as a Spring bean, and component-scan tells Spring where to search so it can automatically register that class in the IoC container.**
