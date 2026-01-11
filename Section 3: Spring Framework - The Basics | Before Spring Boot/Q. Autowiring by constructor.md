# Autowiring by Constructor

---

## Why do we even need “by constructor”?

So far I learned:

* **By name** → matches variable name with bean ID
* **By type** → matches class type

Now Spring gives one more option:

👉 **Autowiring by constructor**

Meaning:

> Spring will inject dependencies **using the constructor**, not setters.

This is useful because:

* Object is created **fully ready**
* Dependency is **mandatory**
* No half-built objects

---

## What “by constructor” really means (simple words)

Spring says:

> “When I create this object, I will call its constructor
> and pass required dependencies inside it.”

So:

* **Constructor MUST exist**
* Constructor parameters = dependencies

---

## Setup (same Car + Specification example)

### Car depends on Specification

```
Car  --->  Specification
```

---

## Step 1: XML configuration

In Car bean:

```
autowire="constructor"
```

This tells Spring:

> “Use constructor to inject dependencies.”

---

## Step 2: First run (why it printed `null`)

At first, your `Car` class had:

* Setter ✔
* **NO constructor** ❌

So Spring thought:

> “You asked me to autowire by constructor…
> but I don’t see any constructor to use 🤷”

Result:

* Object created
* Dependency NOT injected
* `null` printed

### Key lesson

> **Autowiring by constructor without a constructor = nothing gets injected**

---

## Step 3: Adding constructor (the fix)

You added:

```
public Car(Specification specification) {
    this.specification = specification;
}
```

Now Spring is happy 😊

---

## How Spring thinks now (very important)

Let me slow this down.

### Spring’s thinking:

1. Car bean says: `autowire="constructor"`
2. Spring looks at Car constructors
3. Finds constructor with parameter:

   ```
   Specification
   ```
4. Spring searches:

   > “Do I have exactly ONE bean of type Specification?”
5. If yes → inject it into constructor
6. Car object is created **fully initialized**

---

## Why setter is NOT needed here

You tested this 👇
You commented out the setter… and it still worked.

Why?

Because:

* Injection already happened **during object creation**
* Setter is not used at all

### Important rule

> **With constructor autowiring, setter is optional**

---

## Diagram (lock this image in your head)

### Autowiring by Constructor

```
Spring creates Car
        |
        v
Looks at constructor:
Car(Specification spec)
        |
        v
Find bean of type Specification
        |
        v
Inject via constructor
```

---

## The SAME big rule applies (like by-type)

You tried this:

```
<bean id="specification" />
<bean id="specificationOne" />
```

Both are:

* SAME TYPE → Specification

### What happens?

Spring error:

```
Expected single matching bean
but found 2
```

Why?

Because Spring doesn’t know:

> “Which one should I pass into constructor?”

So rule is:

> **Autowiring by constructor requires exactly ONE matching bean**

---

## Fix (again)

Comment one bean → works
Uncomment second bean → error

Simple and predictable.

---

## Comparing all 3 autowiring types (very important table)

| Feature                  | By Name            | By Type    | By Constructor         |
| ------------------------ | ------------------ | ---------- | ---------------------- |
| Matching based on        | Variable name      | Class type | Constructor param type |
| Setter needed            | YES                | YES        | NO                     |
| Constructor needed       | NO                 | NO         | YES                    |
| Multiple beans allowed   | YES (names differ) | NO         | NO                     |
| Null risk                | High               | Low        | Very low               |
| Preferred in Spring Boot | ❌                  | ⚠️         | ✅                      |

---

## Why Spring Boot LOVES constructor injection

This is a **preview**, but important:

* Makes dependency **mandatory**
* Object is always valid
* Easy to test
* No partially-initialized objects

That’s why:

> Spring Boot defaults to constructor injection

(You’ll see this with `@Autowired` later)

---

## Beginner mental shortcut (remember this)

* **Setter injection** → “I’ll give you dependency later”
* **Constructor injection** → “You must have this to exist”

---

## Debug checklist (exam + interview + real life)

If constructor autowiring fails:

1. Is constructor present? ❓
2. Does constructor parameter match bean type? ❓
3. Do I have more than one bean of same type? ❓

---

## One-line recall (final)

> **Autowiring by constructor injects dependencies at object creation time using constructor parameters and requires exactly one matching bean of that type.**
