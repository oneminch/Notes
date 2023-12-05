- All **objects** have:
    - ==Identity== - separates one object from another
    - ==Attributes== - properties
    - ==Behaviors== - methods 
- **Class** - blueprint/template for creating objects.
    - Components of a class:
        - ==Name  / Type== - what it is
        - ==Attributes / Properties / Data== - what describes it 
        - ==Behaviors / Operations / Methods== - what it can do
- OOP is made up of four fundamental pillars:
    - **A**bstraction
        - Contextual model of a real-world object that represents its relevant details.
        - Involves reducing characteristics from something to a set of essential features. 
    - **P**olymorphism
        - Allows us to present the same interface for varying underlying forms.
        - *Dynamic polymorphism* uses method overriding.
        - *Static polymorphism* uses method overloading.
    - **I**nheritance
        - Allows us to reuse our code by basing a new object or class on an existing one.
        - Existing attributes and methods get *inherited*.
        - The existing class is usually known as a superclass or parent class or base class.
        - The newly-created class is usually known as a subclass or child class or derived class.
        - Can be single, where a class is derived from a one superclass (e.g. Java), or multiple, where a class is derived from multiple superclasses (e.g. Python).
    - **E**ncapsulation
        - Can be expressed in two ways:
            - Ability to *encapsulate* state (attributes) and behavior (methods) into a single unit - an object.
            - Ability of an object to hide parts of its internal workings from external code.

- OOP also involves **composition**, which defines a "has a" relationship by storing an object as a variable inside another object. 
    - e.g. an object of type `Car` can be assigned as a variable in an object of type `Person` to establish that `Person` has a `Car`.

- Classes allow us to create our own data types. They act as a blueprint for pieces of data.

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

### Inheritance

```python
class Car:
    def __init__(self, make, model, year):
        self.make = make
        self.model = model
        self.year = year

    def drive(self):
        print("Driving...")

class Battery:
    def __init__(self, size=100):
        self.size = size

    def describe_size(self):
        print(f"The car has {self.size} kWh battery.")

class EV(Car):
    def __init__(self, make, model, year):
        super().__init__(make, model, year)
        self.range = 300
        self.battery = Battery()

    # overrides parent drive() method
    def drive(self):
        print("Quietly driving...")

    def describe_range(self):
        print(f"On a full charge, the {self.year} {self.make} {self.model} has a {self.range} mi range.")

class Gasoline(Car):
    pass	# To avoid empty class error


rivian = EV("Rivian", "R1T", 2022)
rivian.drive()
rivian.describe_range()
rivian.battery.describe_size()
```


---
## Further

### Learn 🧠

- [Programming Foundations: Object-Oriented Design](https://www.linkedin.com/learning/programming-foundations-object-oriented-design-3)

- [Grokking the Low Level Design Interview Using OOD Principles (Educative)](https://www.educative.io/courses/grokking-the-low-level-design-interview-using-ood-principles)
### Resources 🧩

- [tssovi/grokking-the-object-oriented-design-interview (GitHub)](https://github.com/tssovi/grokking-the-object-oriented-design-interview)