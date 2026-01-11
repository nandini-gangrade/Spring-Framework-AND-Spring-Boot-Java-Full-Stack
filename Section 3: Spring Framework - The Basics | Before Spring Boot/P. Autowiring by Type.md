# Autowiring by Type

---

## Why Autowiring by Type exists

Earlier, with **autowiring by name**, Spring was very picky:

> “Variable name must exactly match bean ID”

That works… but it’s fragile:

* rename variable → wiring breaks
* refactor → silent bugs

So Spring gives us something **stronger and safer**:

👉 **Autowiring by TYPE**

---

## What does “by type” actually mean?

Very literal meaning:

> Spring injects a dependency based on the **class type**, not the name.

So Spring asks:

> “This class needs an object of type X.
> Do I have **exactly one bean** of type X?”

If yes → inject it
If no or more than one → error

---

## The same example (Car → Specification)

Nothing fancy. Same setup.

```
Car depends on Specification
```

### Car class (important part)

```
class Car {
    Specification specification;
}
```

Spring only cares about:

* `Specification` (the TYPE)

Not:

* variable name
* setter name
* bean ID name

---

## XML change (the only thing we change)

In the Car bean:

```
autowire="byType"
```

That’s it.

This line tells Spring:

> “Inject dependencies by matching class types.”

---

## How Spring thinks (step by step)

Let me again think like Spring 👇

---

### Step 1: Load XML configuration

Spring loads `autowire-by-type.xml`.

---

### Step 2: Create Specification beans

Let’s say I have this:

```
<bean id="specification" class="Specification" />
<bean id="specificationOne" class="Specification" />
```

So now Spring has:

* 2 beans
* SAME TYPE: `Specification`

Keep this in mind.

---

### Step 3: Create Car bean (autowire by type)

Spring opens `Car` class.

It sees:

```
Specification specification;
```

Spring now asks:

> “I need **one** bean of type Specification.”

---

## ❌ The BIG RULE of Autowiring by Type

> **There must be exactly ONE bean of that type**

### What happens if there are TWO?

Spring gets confused:

```
Expected single matching bean
but found 2:
- specification
- specificationOne
```

And the application **fails to start**.

This is GOOD behavior — Spring is protecting you.

---

## Fixing the error (why commenting works)

When I comment one bean:

```
<bean id="specificationOne" ... />
```

Now Spring sees:

```
Only ONE Specification bean exists
```

So injection succeeds.

---

## Important diagram (lock this in)

### Autowiring by Type flow

```
Car class:
-------------------------
Specification specification;
-------------------------

Spring search:
-------------------------
Find bean of type Specification
-------------------------

✔ ONE found → inject
✖ ZERO found → error
✖ MORE THAN ONE → error
```

---

## What about variable names?

Here’s the **key difference** from by-name.

Let’s say I rename this:

```
Specification specificationOne;
```

And setter:

```
setSpecificationOne(...)
```

### With by-name ❌

* Bean ID must match
* Otherwise → null

### With by-type ✅

* Spring does NOT care about name
* Only cares about type
* Works perfectly

---

## Proof (why your experiment worked)

You did this:

* Variable name ≠ bean name
* Still worked

Why?

Because:

> Spring matched **Specification.class**, not names

That’s the power of by-type.

---

## Does setter still matter?

Yes ✅

Even in autowiring by type:

* Injection still happens via **setter**
* If setter is missing → injection fails or value stays null

### Rule:

> Autowiring ≠ magic
> Setter (or constructor) is still required

---

## Comparing Autowiring by Name vs By Type

| Feature                | By Name                 | By Type                |
| ---------------------- | ----------------------- | ---------------------- |
| Matches                | Variable name ↔ Bean ID | Class type             |
| Sensitive to renaming  | YES ❌                   | NO ✅                   |
| Multiple beans allowed | YES (if names differ)   | NO ❌                   |
| Setter required        | YES                     | YES                    |
| Common errors          | Null injection          | Multiple-bean conflict |

---

## When would I use by-type?

✔ When:

* You have only one implementation
* You want refactor-safe wiring
* Cleaner XML

❌ Avoid when:

* Multiple implementations exist
* You don’t want ambiguity

(That’s where `@Qualifier` comes later)

---

## Real-world intuition (easy memory trick)

Think like this:

* **By name** → “Call this person by their name”
* **By type** → “Call whoever has this job role”

If two people have the same job role → confusion.

---

## Final mental checklist (debugging by type)

If app fails on startup:

1. Do I have **more than one bean of same type**?
2. Did I accidentally copy-paste another bean?
3. Is setter present?

99% of issues are from point #1.

---

## One-line recall (lock it)

> **Autowiring by type injects a dependency only when exactly one bean of that class type exists in the container.**
