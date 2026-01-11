# Autowiring by Name


---

## Why am I learning Autowiring by Name?

Till now, I was **telling Spring explicitly**:

> “This bean needs that bean.”

I did this using:

* `<constructor-arg>`
* `<property ref="...">`

Now I want Spring to:

* **figure out dependencies on its own**
* inject them **automatically**

Autowiring by **name** is the first automatic way to do this.

---

## What does “by name” actually mean?

It literally means:

> Spring matches the **variable name inside the class**
> with the **bean ID name in XML**

If names match → dependency injected
If names don’t match → dependency stays `null`

Very simple rule.

---

## The setup (what classes exist)

I have two classes:

```
Car  → depends on → Specification
```

### Car class (simplified thinking)

```
class Car {
    Specification specification;
}
```

* `specification` is a **dependency**
* Car cannot work properly without it

---

## Earlier (Constructor Injection – what we used before)

Earlier we did this:

```
<constructor-arg ref="carSpecification" />
```

Meaning:

> “Spring, inject this exact bean using constructor.”

But now ❌ we are **not using constructor injection**.

---

## What changes for Autowiring by Name?

### 1️⃣ XML change (MOST IMPORTANT)

In the **Car bean**, I add:

```
autowire="byName"
```

Meaning:

> “Spring, inject all dependencies of this bean by matching names.”

So now XML says:

* I am not telling *which* dependency
* I am only telling *how* to find it (by name)

---

## How Spring thinks (step by step)

Let me think like Spring 👇

### Step 1: Load configuration

Spring reads the XML file.

---

### Step 2: Create Specification bean

```
<bean id="specification" class="Specification">
```

Spring:

* creates Specification object
* calls setters like `setMake()`, `setModel()`

✅ Specification bean ready

---

### Step 3: Create Car bean (autowire by name)

Spring sees:

```
<bean class="Car" autowire="byName">
```

Spring now:

* opens `Car` class
* looks at **fields**

It sees:

```
Specification specification;
```

Field name = `specification`

---

### Step 4: Match names

Spring asks:

> “Do I have a bean with ID = `specification`?”

If YES → inject it
If NO → leave it `null`

That’s it. That’s autowiring by name.

---

## Very important diagram (burn this into brain)

```
Car class:
--------------------------------
Specification specification;
--------------------------------

XML:
--------------------------------
<bean id="specification" ... />
--------------------------------

Name matches → Inject
```

---

## How injection actually happens (important detail)

Even though I did **not** write `<property>`…

👉 Spring still uses **SETTER METHOD** internally.

So this method **must exist**:

```
setSpecification(...)
```

If setter is missing ❌
→ Spring cannot inject
→ value remains `null`

---

## What happens if setter is missing?

If I comment or remove setter:

```
setSpecification(...)
```

Then:

* Spring finds the bean
* But cannot inject it
* `specification` remains `null`
* App crashes with `NullPointerException`

### Rule to remember:

> **Autowiring by name always uses setters**

---

## What if names don’t match?

### Case 1: Variable name changed

```
Specification specificationOne;
```

But XML still has:

```
id="specification"
```

❌ No match
❌ No injection
❌ `null` value

---

### Case 2: Bean ID changed

```
id="carSpecification"
```

But variable name is:

```
specification
```

❌ No match
❌ No injection

---

### Rule (very strict):

```
variable name == bean id
```

Even one extra character breaks it.

---

## What if I have TWO beans with same name?

This is illegal ❌

Spring gets confused:

> “Which one should I inject?”

Result:

* Big scary error
* Application won’t start

So:

> **Bean IDs must be unique**

---

## Using multiple beans correctly (experiment explained)

If I want to use another bean:

```
Specification specificationOne;
```

Then I must change **ALL THREE**:

1. Variable name
2. Setter name
3. Bean ID

Example:

```
setSpecificationOne(...)
id="specificationOne"
Specification specificationOne;
```

Now it works.

---

## Common beginner mistakes (I should remember)

❌ Forgot setter
❌ Bean ID and variable name mismatch
❌ Renamed variable but not setter
❌ Multiple beans with same ID

If value is `null` → check **name + setter**

---

## Why is Autowiring by Name useful?

✔ Less XML
✔ No `<property>` tags
✔ Easy to understand
✔ Predictable behavior

But…

❌ Renaming variables can silently break wiring
❌ Large apps prefer other types (like by constructor)

---

## How this connects to Spring Boot (preview)

In Spring Boot:

* Autowiring is mostly done using **annotations**
* But the **same rules apply**
* Names still matter

So understanding this now = fewer bugs later.

---

## Final mental summary (me revising)

* Autowiring by name matches **field name** with **bean ID**
* Setter is mandatory
* Names must match exactly
* Injection happens automatically
* No constructor injection here

---

## One-line recall (important)

> **Autowiring by name injects a dependency only when the variable name and bean ID are exactly the same.**
