- In the context of [[OOP]], a static method can be called either directly on a class or on an instance of a class.

**Python**

```python
class Car:
    @staticmethod
    def drive():
        print("Vroooom!")


Car.drive()
Car().drive()
drive()
```

**C#**

```cs
class Car {
    public static void drive() {
        System.Console.WriteLine("Vroooom!");
    }
}

class Program {
    static void Main() {
        Car.drive();
    }
}
```