# Creating the First Spring Bean (XML Configuration)

---

## Where we are now

The project is already set up as a **Spring-enabled Maven project**.

That means:

* `pom.xml` already contains **Spring Core** and **Spring Context**
* Spring framework features are now available
* We can start creating **beans** and let **Spring manage objects**

---

## Goal of this section

* Create a **simple Java class**
* Tell Spring to manage its object
* Load Spring Container
* Ask Spring for the object
* Understand how values are injected into the bean

---

## Step 1: Create a simple Java class (Bean class)

This class will be managed by Spring.

### Package and class

Package:

```
car.example.bean
```

Class name:

```
MyBean
```

---

### `MyBean.java`

```java
package car.example.bean;

public class MyBean {

    private String message;

    // Setter method
    public void setMessage(String message) {
        this.message = message;
    }

    // Method to display message
    public void showMessage() {
        System.out.println(message);
    }

    @Override
    public String toString() {
        return "MyBean{message='" + message + "'}";
    }
}
```

---

### What this class contains

* `message` → class variable
* `setMessage()` → setter used by Spring
* `showMessage()` → prints the message
* `toString()` → prints object details

This is a **very simple bean**, just enough to understand Spring basics.

---

## Step 2: Create Spring XML configuration file

Spring needs instructions about:

* which class to manage
* what name (ID) to give it
* what values to initialize

These instructions are given using a **configuration file**.

---

### File location

Create the file inside:

```
src/main/resources
```

File name:

```
applicationBeanContext.xml
```

---

## Step 3: XML boilerplate (required setup)

Spring XML needs namespace and schema details.

### `applicationBeanContext.xml`

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">

</beans>
```

---

### What this part does

* Defines XML version and encoding
* Sets Spring **beans namespace**
* Enables Spring to correctly read and validate bean definitions

Without this, Spring XML configuration will not work.

---

## Step 4: Define the bean in XML

Now we tell Spring **which class to manage**.

---

### Bean definition added inside `<beans>`

```xml
<bean id="myBean"
      class="car.example.bean.MyBean">
</bean>
```

---

### Meaning of each part

* `id="myBean"`

  * This is the **name** used to request the object from Spring

* `class="car.example.bean.MyBean"`

  * Fully qualified class name
  * Tells Spring where the class is located

---

### Diagram: Bean definition flow

```
applicationBeanContext.xml
        |
        |-- bean id="myBean"
        |-- class="car.example.bean.MyBean"
        |
Spring Container
        |
Creates and manages MyBean object
```

---

## Step 5: Create main application class

This class will:

* load Spring Container
* request the bean
* use the bean

---

### `App.java`

```java
package car.example;

import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

import car.example.bean.MyBean;

public class App {

    public static void main(String[] args) {

        // Step 1: Load Spring context
        ApplicationContext context =
                new ClassPathXmlApplicationContext("applicationBeanContext.xml");

        // Step 2: Get bean from Spring container
        MyBean myBean = (MyBean) context.getBean("myBean");

        // Step 3: Use the bean
        System.out.println(myBean);
    }
}
```

---

## What happens internally (important)

### Step 1: Load Spring Container

```java
ApplicationContext context =
        new ClassPathXmlApplicationContext("applicationBeanContext.xml");
```

* `ApplicationContext` → Spring container interface
* `ClassPathXmlApplicationContext` → XML-based implementation
* Loads bean definitions from classpath XML file
* Creates and configures beans

---

### Step 2: Get bean from container

```java
MyBean myBean = (MyBean) context.getBean("myBean");
```

* `getBean("myBean")` asks Spring for the object
* Spring returns the managed object
* Type casting is required

---

### Step 3: Print the object

```java
System.out.println(myBean);
```

This calls `toString()` of `MyBean`.

---

## Output at this stage

```
MyBean{message='null'}
```

---

### Why message is `null`

* `message` was never initialized
* No setter was called
* No value was provided in XML
* Default value for `String` is `null`

---

## Step 6: Initialize property using XML

Spring allows setting values using `<property>` tag.

---

### Updated bean definition

```xml
<bean id="myBean"
      class="car.example.bean.MyBean">

    <property name="message" value="I am a first bean"/>

</bean>
```

---

### What this means

* `name="message"` → class variable name
* `value="I am a first bean"` → value to assign
* Spring looks for:

  * `setMessage()` method
  * calls it automatically

---

### Diagram: Property injection

```
Spring Container
       |
       |-- creates MyBean
       |-- finds property "message"
       |-- calls setMessage("I am a first bean")
       |
Fully initialized MyBean
```

---

## Output after property injection

```
MyBean{message='I am a first bean'}
```

---

## Important rule: Setter is mandatory

If `setMessage()` is removed or commented:

```java
// public void setMessage(String message) {
//     this.message = message;
// }
```

Spring will fail during startup.

---

### Error reason

Spring:

* finds `<property name="message">`
* looks for `setMessage()`
* cannot find it
* throws error and stops application

---

### Error meaning (simplified)

* Property exists
* Setter does not exist
* Bean cannot be created
* Application ends

---

## Why this is Dependency Injection

* Object creation is done by Spring
* Property values are injected by Spring
* Code does not manually create objects
* Configuration controls behavior

---

### Diagram: Dependency Injection flow

```
XML Configuration
       |
Spring Container
       |
Creates object
Injects values
       |
Provides object when requested
```

---

## Final understanding

* Bean = Java object managed by Spring
* XML configuration tells Spring what to manage
* ApplicationContext loads and controls everything
* `getBean()` gives ready-to-use objects
* `<property>` injects values using setters

---

## One-line recall

> **Spring creates the object, injects values using setters from XML, and provides the fully ready bean when requested.**
