# Setter Injection

---

## What is Setter Injection?

**Setter Injection** is a type of **Dependency Injection** where dependencies are provided to the dependent class **through setter methods**.

Instead of passing the dependency through the constructor, the dependent class:

* exposes a setter method
* Spring calls that setter and injects the dependency after the object is created

---

## Key Points from the Slide

* Dependencies are provided to the dependent class through setter methods
* The dependent class exposes setter methods for each dependency
* Setter injection allows flexibility because dependencies can be changed or updated **after** the object is instantiated

---

## Difference from Constructor Injection (Context)

In **constructor injection**:

* Dependency is mandatory
* Object cannot be created without dependency

In **setter injection**:

* Dependency is optional
* Object is created first
* Dependency is injected later using setter

---

## Scenario We Are Building

We will again use:

* `Specification` class (dependency)
* `Car` class (dependent)
* `App` class
* XML configuration

But now:

* **No constructor injection**
* **Setter method will be used**

---

## Package Structure

```
car.example.setter.injection
│
├── App.java
├── Car.java
└── Specification.java
```

---

## Specification Class (Same as Before)

```java
package car.example.setter.injection;

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

## Car Class (Setter Injection)

Here we **remove the constructor** and add a setter.

```java
package car.example.setter.injection;

public class Car {

    private Specification specification;

    // Setter Injection
    public void setSpecification(Specification specification) {
        this.specification = specification;
    }

    public void displayDetails() {
        System.out.println("Car details:");
        System.out.println(specification.toString());
    }
}
```

Important observations:

* No constructor is defined
* Dependency is injected using `setSpecification`
* Object can exist without dependency initially

---

## XML Configuration File

Create this under `resources`:

**application-setter-injection.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <!-- Specification Bean -->
    <bean id="carSpecification"
          class="car.example.setter.injection.Specification">
        <property name="make" value="Toyota"/>
        <property name="model" value="Corolla"/>
    </bean>

    <!-- Car Bean using Setter Injection -->
    <bean id="myCar"
          class="car.example.setter.injection.Car">
        <property name="specification" ref="carSpecification"/>
    </bean>

</beans>
```

### Important XML Details

* `<property>` is used instead of `<constructor-arg>`
* `name="specification"` matches the setter name `setSpecification`
* `ref="carSpecification"` refers to another bean

---

## App Class

```java
package car.example.setter.injection;

import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class App {

    public static void main(String[] args) {

        ApplicationContext context =
                new ClassPathXmlApplicationContext("application-setter-injection.xml");

        Car myCar = (Car) context.getBean("myCar");

        myCar.displayDetails();
    }
}
```

---

## Execution Flow

```
1. Application starts
2. Spring loads XML configuration
3. Spring creates Car object (no constructor dependency)
4. Spring creates Specification object
5. Spring calls setSpecification()
6. Dependency is injected
7. Car is ready to use
```

---

## Visual Flow Diagram

```
Spring Container
      |
      |
Creates Car Bean
      |
      |
Creates Specification Bean
      |
      |
Calls setSpecification()
      |
      |
Car Ready
```

---

## Output

```
Car details:
Specification{make='Toyota', model='Corolla'}
```

---

## Why This is Setter Injection

* Dependency is injected using a setter method
* Object creation happens first
* Dependency can be changed later if needed
* Uses `<property>` tag in XML

---

## When Setter Injection is Useful

* When dependency is optional
* When dependency may change
* When flexibility is more important than strict enforcement

---

## Key Takeaways

* Setter Injection injects dependencies using setter methods
* Uses `<property>` tag in XML
* Dependency injection happens after object creation
* More flexible than constructor injection
* Dependent class must expose setters

---

## One-line Recall

> **Setter Injection injects dependencies after object creation using setter methods, allowing flexibility.**
