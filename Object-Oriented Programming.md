---
alias: OOP
---

## Introduction

- All **objects** have:
    - ==Identity== - Separates one object from another
    - ==Attributes== - Properties
    - ==Behaviors== - Methods 

- **Class** - blueprint/template for creating objects.
    - Components of a class:
        - ==Name  / Type== - what it is
        - ==Attributes / Properties / Data== - what describes it 
        - ==Behaviors / Operations / Methods== - what it can do
    - Classes allow us to create our own data types.

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y
        self.z = 0
    
    def update_z(self, value):
        self.z = value
    
    def increment_y(self, num):
        self.y += num
      
    def display(self):
        print(f"({self.x}, {self.y}, {self.z})")

# Ways to instantiate objects,
# modify attributes and invoke methods

point_1 = Point(15, 25)

point_2 = Point(15, 25)
point_2.x = 25
point_2.y = 35
point_2.z = 45
point_2.display()

point_3 = Point(15, 25)
point_3.update_z(10)
```

## The Four Fundamental Pillars of OOP

### Abstraction

- Contextual model of a real-world object that represents its relevant details.
- Involves reducing characteristics from something to a set of essential features. 

### Polymorphism

- Allows us to present the same interface for varying underlying forms.
- *Dynamic polymorphism* uses method overriding.
- *Static polymorphism* uses method overloading.

#### Method Overloading

- Method overloading can be implemented in two different ways that involve implementing two or more methods with the same name. 
- One difference is in the numbers of arguments the methods take.

```java
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
    
    public int add(int a, int b, int c) {
        return a + b + c;
    }
}
```

- Another difference is in the types of the arguments the methods take.

```java
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
    
    public double add(double a, double b) {
        return a + b;
    }
}
```

- It’s also valid to define a class with both types of method overloading:

```java
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
    
    public int add(int a, int b, int c) {
        return a + b + c;
    }
    
    public double add(double a, double b) {
        return a + b;
    }
}
```

> [!note]
> It’s not possible to have two method implementations that differ only in their return types.

- Overloading can also be applied to class [[Constructor|constructors]].

```java
public class Person {
    private String name;
    private int age;

    // No-argument constructor
    public Person() {
        name = "Unknown";
        age = 0;
    }

    // Constructor with name parameter
    public Person(String name) {
        this.name = name;
        age = 0;
    }

    // Constructor with name and age parameters
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

- Method overloading provides features such as type promotion and static binding.

#### Method Overriding

- With method overriding, we can provide fine-grained implementations of methods in subclasses originally defined in a base class.

```java
public class Vehicle {
    public String accelerate(long mph) {
        return "Vehicle Accelerating at: " + mph + " MPH.";
    }
    
    public String stop() {
        return "Vehicle Stopped.";
    }
}
```

```java
public class ATV extends Vehicle {
    @Override
    public String accelerate(long mph) {
        return "ATV Accelerating at: " + mph + " MPH.";
    }
}
```

> [!note]
> Since the compiler can’t determine what method to call at compile time (as both the base class and the subclasses define the same methods), the compiler needs to check the type of object to know what method should be called. 
> 
> This check happens at runtime, and because of that method overriding is a typical example of **dynamic binding**.

### Inheritance

- Allows us to reuse our code by basing a new object or class on an existing one.
- Existing attributes and methods get *inherited*.
- The existing class is usually known as a superclass or parent class or base class.
- The newly-created class is usually known as a subclass or child class or derived class.
- When we extend a class, we form an "IS-A" relationship.
- Can be single, where a class is derived from a one superclass (e.g. Java), or multiple, where a class is derived from multiple super classes (e.g. Python).

```java
class Car {
    protected String make;
    protected String model;
    protected int year;

    public Car(String make, String model, int year) {
        this.make = make;
        this.model = model;
        this.year = year;
    }

    public void drive() {
        System.out.println("Driving...");
    }
}

class Battery {
    private int size;

    public Battery() {
        this.size = 100;
    }
    
    public Battery(int size) {
        this.size = size;
    }

    public void describeSize() {
        System.out.print("The car has " + this.size + " kWh battery.");
    }
}

class EV extends Car {
    private int range;
    private Battery battery;

    public Car(String make, String model, int year) {
        super(make, model, year);
        this.range = 300;
        this.battery = new Battery();
    }

    public void drive() {
        System.out.println("Quietly Driving...");
    }

    public Battery getBattery() {
        return this.battery;
    }

    public void describeRange() {
        System.out.print("On a full charge, the " + this.year + " " + this.make + " " + this.model + " has a " + this.range + "mi range.")
    }
}
```

```java
EV rivian = new EV("Rivian", "R1T", 2022);

rivian.drive();
rivian.describeRange();
rivian.battery.describeSize();
```

### Encapsulation

- Can be expressed in two ways:
    - Ability to *encapsulate* state (attributes) and behavior (methods) into a single unit - an object.
    - Ability of an object to hide parts of its internal workings from external code.

## Composition

- OOP also involves **composition**, which defines a "HAS-A" relationship by storing an object as a variable inside another object. 
    - e.g. an object of type `Car` can be assigned as a variable in an object of type `Person` to establish that `Person` has a `Car`.

---

## Further

### Learn 🧠

- [Object-Oriented Design (Coursera)](https://www.coursera.org/learn/object-oriented-design)

- [Intro to Object Oriented Programming (YouTube)](https://www.youtube.com/watch?v=SiBw7os-_zI)

- [Programming Foundations: Object-Oriented Design](https://www.linkedin.com/learning/programming-foundations-object-oriented-design-3)

- [Grokking the Low Level Design Interview Using OOD Principles (Educative)](https://www.educative.io/courses/grokking-the-low-level-design-interview-using-ood-principles)

### Read 📄

- [Object-Oriented Programming: A Primer](https://aigents.co/data-science-blog/publication/object-oriented-programming-a-primer)

### Resources 🧩

- [tssovi/grokking-the-object-oriented-design-interview (GitHub)](https://github.com/tssovi/grokking-the-object-oriented-design-interview)