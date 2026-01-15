## 🧠 @Qualifier Annotation

---

## What this video is about (me talking to myself)

> “Okay, @Autowired works fine… but what if Spring finds **more than one matching bean**? How do I tell Spring *which one exactly* I want?”

That’s where **@Qualifier** comes in.

---

## The real problem this video solves

In **real / large projects**:

* You don’t have just one bean of a type
* You may have **multiple beans of the same class**

Example:

```
Employee employee1
Employee employee2
```

Both are:

* Type → `Employee`
* Managed by Spring
* Registered as beans

Now Spring is confused 🤯

---

## What happens without @Qualifier?

Let’s say in `Manager` I write:

```
@Autowired
private Employee employee;
```

Spring says:

> “Wait… I see 2 Employee beans. Which one do you want?”

Result:
❌ **Error: No unique bean definition**

Spring cannot guess.

---

## What is @Qualifier? (simple meaning)

`@Qualifier` tells Spring:

> “Yes, inject by type… but also match this **bean name**.”

So now Spring:

1. Looks at type
2. Looks at bean name
3. Injects the **exact one** you want

---

## How @Qualifier is used (syntax)

```
@Autowired
@Qualifier("employee")
private Employee employee;
```

Meaning:

> “Spring, inject the Employee bean whose name is **employee**.”

---

## Diagram – Problem without @Qualifier

```
Spring Container
   |
   |-- employee (Employee)
   |-- employeeOne (Employee)
   |
   |-- Manager  --->  ❌ Confused
```

---

## Diagram – With @Qualifier

```
Spring Container
   |
   |-- employee (Employee)   ✔️
   |-- employeeOne (Employee)
   |
   |-- Manager
        |
        |-- @Qualifier("employee")
```

Now Spring knows **exactly** what to inject.

---

## Important rule I learned

> **@Qualifier works with bean name, not class name**

If bean name does not exist → error.

---

## What happens if I give wrong qualifier?

Example:

```
@Qualifier("employeeX")
```

But no bean named `employeeX` exists.

Result:
❌ **No qualifying bean available**

This is expected behavior.

---

## When do I REALLY need @Qualifier?

I need `@Qualifier` **only when**:

* Multiple beans of same type exist
* Spring cannot decide automatically

If:

* Only one bean of that type exists
  → `@Autowired` alone is enough

---

## How beans usually get names (important recall)

By default:

* Class `Employee` → bean name = `employee`
* First letter lowercase

Custom name example:

```
@Component("employeeOne")
```

Then qualifier must match:

```
@Qualifier("employeeOne")
```

---

## Relationship with @Autowired (mental model)

* `@Autowired` → **inject by type**
* `@Qualifier` → **filter by name**

Together:

> “Inject this type, but only this named bean.”

---

## Interview-friendly explanation (in my own words)

> “@Qualifier is used along with @Autowired to resolve ambiguity when multiple beans of the same type are present in the Spring container.”

---

## 🧠 One-Line Recall (VERY IMPORTANT)

> **@Qualifier is used with @Autowired to specify exactly which bean to inject when multiple beans of the same type exist.**
