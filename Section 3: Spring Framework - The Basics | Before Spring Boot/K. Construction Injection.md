# Constructor Injection

---

## What is Constructor Injection?

**Constructor Injection** is a type of **Dependency Injection** where dependencies are provided to the dependent class **through its constructor**.

In simple terms:

* The dependency is passed as an argument to the constructor
* The object cannot be created unless its dependency is available

That’s why it’s called **constructor injection** — because the constructor is used to inject the dependency.

---

## Key Points from the Concept

* Dependencies are provided to the dependent class through its constructor
* Dependencies are passed as arguments when the object is instantiated
* Constructor injection ensures that the dependencies are available **at the time of object creation**

This makes the object fully ready to use right after it is created.

---

## Scenario We Are Building

We will create:

* a **Specification** class (holds car details)
* a **Car** class (depends on Specification)
* an **App** class (loads Spring context)
* an **XML configuration file** (defines beans and constructor injection)

So the dependency relationship looks like this:

```
Car  ---- depends on ---->  Specification
```

Spring will inject `Specification` into `Car` using **constructor injection**.

---

## Package Structure

```
car.example.constructor.injection
│
├── App.java
├── Car.java
└── Specification.java
```

---

## Specification Class

This class stores details about a car.

```java
package car.example.constructor.injection;

public class Specification {

    private String make;
    private String model;

    public String getMake() {
        return make;
    }

    public void setMake(String make) {
        this.make = make;
    }

    public String getModel() {
        return model;
    }

    public void setModel(String model) {
        this.model = model;
    }

    @Override
    public String toString() {
        return "Specification{" +
                "make='" + make + '\'' +
                ", model='" + model + '\'' +
                '}';
    }
}
```

---

## Car Class (Dependent Class)

The `Car` class depends on `Specification`.

```java
package car.example.constructor.injection;

public class Car {

    private Specification specification;

    // Constructor Injection
    public Car(Specification specification) {
        this.specification = specification;
    }

    public void displayDetails() {
        System.out.println("Car details:");
        System.out.println(specification.toString());
    }
}
```

Important things to notice:

* `Specification` is not created using `new`
* It is received through the constructor
* This makes `Car` loosely coupled

---

## XML Configuration File

Create this file under `resources`:

**constructor-injection.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <!-- Specification Bean -->
    <bean id="carSpecification"
          class="car.example.constructor.injection.Specification">
        <property name="make" value="Toyota"/>
        <property name="model" value="Corolla"/>
    </bean>

    <!-- Car Bean with Constructor Injection -->
    <bean id="myCar"
          class="car.example.constructor.injection.Car">
        <constructor-arg ref="carSpecification"/>
    </bean>

</beans>
```

### What is happening here?

* `carSpecification` is defined first because it is a dependency
* `myCar` needs `Specification`
* `<constructor-arg>` tells Spring:

  > pass this bean as a constructor argument

---

## App Class (Main Class)

```java
package car.example.constructor.injection;

import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class App {

    public static void main(String[] args) {

        ApplicationContext context =
                new ClassPathXmlApplicationContext("constructor-injection.xml");

        Car myCar = (Car) context.getBean("myCar");

        myCar.displayDetails();
    }
}
```

---

## Execution Flow (Important)

```
1. Application starts
2. Spring reads constructor-injection.xml
3. Spring creates Specification bean
4. Spring finds Car constructor
5. Spring injects Specification into Car
6. Car object is created
7. Car is ready to use
```

---

## Visual Flow Diagram

```
Spring Container
      |
      |
Creates Specification Bean
      |
      |
Passes it to Car Constructor
      |
      |
Creates Car Bean
      |
      |
App uses Car
```

---

## Output

```
Car details:
Specification{make='Toyota', model='Corolla'}
```

---

## Why This is Constructor Injection

* Dependency is injected through the constructor
* Object cannot exist without its dependency
* Dependency is guaranteed at creation time

This is exactly what constructor injection is meant for.

---

## Key Takeaways

* Constructor Injection injects dependencies via constructor arguments
* Dependencies are mandatory
* Spring uses `<constructor-arg>` in XML
* Ensures the object is fully initialized at creation time
* Encourages strong, predictable object design

---

## One-line Recall

> **Constructor Injection ensures that required dependencies are available the moment an object is created.**
