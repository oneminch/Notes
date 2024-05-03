## Concepts

- Testing
    - JUnit
    - JMeter
- Build Tools
    - Maven
    - Gradle
- Web
    - Java EE / Jakarta EE
        - https://www.youtube.com/watch?v=l1Y-mFWpVm0
        - Servlets, JSP
        - EJB, JPA, JMS
        - Hibernate, JDBC
    - Making API Requests
        - https://www.youtube.com/watch?v=9oq7Y8n1t00
    - [[Spring]]
    - Rest, SOAP, JAX-RS, JAX-WS
- Databases
    - ORMs
        - JPA
        - Spring Data JPA
        - Hibernate
- Containerization and Deployment
    - Docker
    - Kubernetes
    - Cloud platforms (AWS, Azure, GCP)

---

## Intro

- Java is a general-purpose, class-based, [[Object-Oriented Programming]] language.
    - [[Statically-Typed Language|Strongly Typed]],
    - Platform-independent
    - Multi-threaded
- It combines the power of [[Compiled Language|compiled]] languages with the flexibility of [[Interpreted Language|interpreted]] languages.
- **Toolkit**
    - **JDK (Java Development Kit)** includes tools like Java compiler (javac), Java runtime (JRE), javadoc etc.
    - **JRE (Java Runtime Environment)** provides classes, libraries and the JVM needed to run Java programs.
    - **JVM (Java Virtual Machine)** is responsible for executing bytecode generated from Java source code.
        - Provides portability - Write Once, Run Anywhere (WORA)
        - Java Code (`.java`) -> Compiler (`javac`) -> Byte Code (`.class`) -> JVM -> JRE
            - `javac App.java` (Compile) -> `java App` (Execute)
    - **JShell** is the command line REPL for Java.

```java
// HelloWorld.java
public class HelloWorld {
    /* Entry Point of a Java Program */
    public static void main(String[] args) { /* ... */ }
}
```

## Data Types

### Primitives

- **Integers**
    - `byte` (1 byte)
    - `short` (2 bytes)
    - `int` (4 bytes)
    - `long` (8 bytes)
- **Characters** (Unicode)
    - `char` (2 bytes)
- **Floating Point Numbers**
    - `float` (4 bytes)
    - `double` (8 bytes)
- **Boolean**
    - `boolean` (`true` or `false`)

```java
byte a = 12;
short b = 89;
int dec = 9;
int bin = 0b101;
int hex = 0x7E;
long d = 345l;

char c = 'c';
c++; // 'b'

float num1 = 2.5f;
double num2 = 2.5;
double num3 = 2.5d;
double num4 = 2e10;

boolean isTrue = true;
```

> [!note]
> - Numeric ranges of a certain type are from $-2^{(n - 1)}$ to $-2^{(n - 1)} - 1$, where `n` is the number of bits.
> - To increase readability, numbers can be separated with `_`; trailing zeros can be shortened using exponentiation. e.g. `1_000_000`

#### Operators

- **Arithmetic**: `+`, `-`, `/`, `*`, `%`, `++`, `--`

> [!note]
> [[Prefix vs. Postfix Increment|Prefix & postfix increment]] operations behave similarly to that of [[JavaScript]].

- **Comparison**: `<`, `<=`, `>`, `>=`, `==`, `!=`
- **Logical**: `&&`, `||`, `!`

#### Wrapper Objects

- Special classes that "wrap" around primitive data types.
- Provide an object representation of those primitive types. 
- Are [[immutable]].
- Allow primitive data types to be treated as objects, enabling them to be used in contexts where objects are required, such as in collections, generics, and method parameters.
- Purposes:
    - Provide object representation of primitive data types, allowing them to be used in OOP contexts.
    - Provide utility methods for converting between primitive types and their corresponding wrapper class objects (e.g., Integer.parseInt(), Double.valueOf(), etc.).
    - Provide constants and methods related to the respective primitive data type (e.g., MIN_VALUE, MAX_VALUE, etc.).
- Java provides eight wrapper classes, one for each primitive data type:
    - `Boolean` for `boolean`
    - `Byte` for `byte`
    - `Character` for `char`
    - `Short` for `short`
    - `Integer` for `int`
    - `Long` for `long`
    - `Float` for `float`
    - `Double` for `double`
- Java also provides automatic boxing and unboxing mechanisms to simplify the conversion between primitive types and their corresponding wrapper class objects. 

> [!note]
> Boxing is the automatic conversion of a primitive value to its wrapper class object, while unboxing is the automatic conversion of a wrapper class object to its primitive value.

```java
// Boxing
Integer intObj = Integer.valueOf(42);
// OR Integer intObj = 42; (autoboxing)

// Unboxing - Converting wrapper object to primitive
int primitiveInt = intObj.intValue(); 
// OR int primitiveInt = intObj; (autounboxing)

/* --------------------- */

Integer maxInt = Integer.MAX_VALUE;                // 2147483647
String binaryString = Integer.toBinaryString(42);  // 101010

/* --------------------- */

List<Integer> intList = new ArrayList<>();
intList.add(10);                  // Autoboxing
intList.add(Integer.valueOf(20)); // Explicit Boxing

for (Integer num : intList) {
    System.out.println(num);   // Autounboxing
}

/* --------------------- */

int parsedInt = Integer.parseInt("42");           // 42
double parsedDouble = Double.parseDouble("3.14"); // 3.14
```

### Non-primitive Types / Reference Types

- Reference types are nullable, thus can be assigned a value of `null`.
    - `null` represents an absence of value.
    - Accessing a `null` reference value will compile without errors, but will throw a runtime exception (`NullPointerException`).
- A `NullPointerException` is thrown when trying to access a reference variable which is `null` but requires an object.

```java
int[] nums = null;

nums.Length;  // NullPointerException

if(arr != null) {
    System.out.println(arr.length);
} else {
    /* ... */
}
```

#### Strings

- By default, strings are [[immutable]] in Java.

```java
// Strings
String firstName = new String("John");
String lastName = "Doe";
```

- Two string variables storing the same value have the same reference, i.e. there are no duplicate values stored in the heap.

```java
String s1 = "Java";
String s2 = "Java";

System.out.print(s1 == s2); // true
```

- **Mutable strings** can be created using `StringBuffer` or `StringBuilder`.

> [!note] `StringBuffer` vs. `StringBuilder`
> There are no significant difference between `StringBuffer` & `StringBuilder`, except that `StringBuffer` is thread-safe while `StringBuilder` isn't. Because of that, `StringBuffer` is slower.

```java
StringBuffer s = new StringBuffer("Java");
```

#### Arrays

- In Java, arrays are [[Static Arrays|fixed-size]], and [[homogeneous]].

```java
// Creating Arrays
int[] nums = new int[3];           // [0, 0, 0]
boolean[] bools = new boolean[2];  // [false, false]
String[] strs = new String[2];     // [null, null]

int[] nums2 = {1, 2, 3, 4, 5};
String[] strs2 = {"John", "Jane"};

// Position of Square Brackets
int nums[] = {1, 2, 3};   // Also Valid Syntax

// 2D Array
int[][] matrix = new int[3][4];

// Jagged Array
int[][] jaggedArray = new int[2][];
jaggedArray[0] = new int[7];
jaggedArray[1] = new int[4];

// 3D Array
int[][][] matrix = new int[3][4][5];
```

#### Classes

```java
Person john = new Person("John Doe");
Person jane = john;

john.name = "Jane Doe";

System.out.print(john.name);  // Jane Doe
System.out.print(jane.name);  // Jane Doe
```

#### Interface

- An interface is a blueprint or contract that defines a set of abstract methods and constants.
    - Specifies the behavior of a class without providing the implementation details. 
    - Declared using the `interface` keyword.
    - Can only contain abstract methods, which are methods without any implementation. 
        - Can also have default and static methods (Java 8), and `private` and `private static` methods (Java 9).
        - All the methods in an interface are public and abstract by default.
    - Can only have static final variables (constants), and all variables are implicitly `public`, `static`, and `final`.
        - That means they have to be assigned a value at definition.
    - Used to achieve abstraction.
    - Allow a class to implement multiple interfaces, providing a way to achieve [[multiple inheritance]], which is not possible with classes.
    - Promote loose coupling between classes by defining a contract that classes must follow, without specifying the implementation details.
    - Cannot be instantiated directly. 
        - They are *implemented* by classes, which provide the actual implementation of the abstract methods.

```java
public interface Printable {
    void print(String message);
}

public class Printer implements Printable {
    @Override
    public void print(String message) {
        System.out.println("Printing: " + message);
    }
}

public class Main {
    public static void main(String[] args) {
        Printable printer = new Printer();
        printer.print("Hello, World!");
    }
}
```

- An interface can extend multiple other interfaces.
    - It inherits the abstract method definitions from all the parent interfaces.
    - A class that implements the child interface must then implement all the methods defined in the parent interfaces as well as the child interface.

```java
interface Calc {
    void add();
}

interface SciCalc extends AddCalc { /*...*/ }

class MyClass implements SciCalc { /*...*/ }
```

- It's possible for a class to implement multiple interfaces with identical method definitions.

```java
interface X {
    void commonMethod();
}

interface Y {
    void commonMethod();
}

class MyClass implements X, Y {
    @Override
    public void commonMethod() {
        System.out.println("Common Method Implemented!");
    }
}
```

- Unlike abstract classes, adding new methods to an interface (using default or static methods) maintains backward compatibility, as existing implementing classes do not need to be modified.

> [!important] 
> - By default, a class that doesn't full implement an interface is an abstract class.
> - A class cannot implement multiple interfaces with the same methods having the same signature but different return types. It results in an error. But, it's possible to implement interfaces with methods of the same name and return type but different parameter list.

##### Functional Interface

- Contains exactly one abstract method.
- Also known as Single Abstract Method (SAM) interfaces.
- Can be annotated using `@FunctionalInterface`.
- Enable a more [[Functional Programming]] style in Java.
- Allow for the use of lambda expressions and method references to provide implementations of the SAM.

##### Marker Interface

- Contains no methods.

### Type Casting / Conversion

#### Primitive Type Casting

```java
byte a = 127;
int b = 14;

// Implicit (Conversion)
a = b; // ⛔
b = a; // ✅ 

// Explicit (Casting)
a = (byte)b;
``` 

- Type casting can be lossy.
    - e.g. A float casted to an integer will lose its decimal points.

- **Widening Casting** (automatic) - convert a smaller type to a larger size type.
    - `byte` -> `short` -> `char` -> `int` -> `long` -> `float` -> `double`
- **Narrowing Casting** (manual) - convert a larger type to a smaller size type.
    - `double` -> `float` -> `long` -> `int` -> `char` -> `short` -> `byte`

#### Type Promotion

```java
byte a = 10;
byte b = 20;

int c = a * b; // 200 (Outside byte range)
```

#### Object Type Casting

- Upcasting and downcasting allow for flexible and polymorphic behavior when dealing with objects of different class types.

##### Upcasting

- Casting an object of a subclass to its parent or superclass type.
- Allows an instance of a subclass access to the methods defined in the superclass. However, methods specific to the subclass cannot be accessed through the upcast reference.
- Implicit and safe operation that does not require an explicit cast.

```java
class Vehicle {
    void drive() {
        System.out.println("Driving a vehicle...");
    }
}

class Car extends Vehicle {
    void accelerate() {
        System.out.println("Speeding up a car...");
    }
}
```

```java
public class Main {
    public static void main(String[] args) {
        Car car = new Car();     // Object of subclass
        Vehicle vehicle = car;   // Upcasting - Treating Car as Vehicle
        // vehicle.drive();      // ✅, drive() present in Vehicle
        // vehicle.accelerate(); // ⛔, accelerate() specific to Car
    
        goForARide(vehicle);
        goForARide(car);
    
        /*
        Output:
            Driving a vehicle...
            Driving a vehicle...
        */
    }

    public static void goForARide(Vehicle v) {
        v.drive();
    }
}
```

> [!important]
> - The *type* of variable determines which methods can be called. 
>     - e.g. `drive()` can be called on any `Vehicle`.
> 
> - The specific type of the object a variable is referring to determines which specific implementation of a method will be used when it's called. 
>     - e.g. If `drive()` has been overridden from the subclass `Car`, `Car`'s implementation of `drive()` will be used at run time.

##### Downcasting

- Casting an object of a superclass type to its child or subclass type.
- An explicit operation that requires an explicit cast.
    - Can lead to runtime exceptions if not performed correctly.
- Should be performed with caution, as it can lead to a `ClassCastException` if the object being downcast is not an instance of the target subclass type. 
    - It is recommended to use the `instanceof` operator to check the object's type before downcasting.

```java
public class Main {
    public static void main(String[] args) {
        Vehicle vehicle = new Car();  // Upcasting
        Car car = (Car) vehicle;      // Downcasting
        // car.drive();               // ✅, drive() present in Vehicle
        // car.accelerate();          // ✅, accelerate() specific to Car
    
        goForARide(vehicle);
        goForARide(car);

        /*
        Output:
            Driving a vehicle...
            Speeding up a car...
            Driving a vehicle...
            Speeding up a car...
        */
    }
    
    public static void goForARide(Vehicle v) {
        v.drive();

        if (v instanceof Car) {
            Car c = (Car) v;
            c.accelerate();
        }
    }
}
```

---

> [!note]
> - Primitives are predefined in Java, while non-primitives are not (except for `String`).
>     - They are created by the developer.
> - Non-primitives have methods for performing certain operations, while primitives don't.
> - A primitive always has a value, while a non-primitive can be `null` (absence of value).
> - A primitive type starts with a lowercase letter, while a non-primitive type starts with an uppercase letter.

## Control Flow

### Conditionals

**If/Else**
```java
if (condition) {
    /* Code Block */
} else if (anotherCondition) {
    /* Code Block */
} else {
    /* Code Block */
}
```

- As with [[JavaScript|JS]], curly brackets are optional for single-line expressions inside conditionals.

**Switch Statements**

```java
switch (condition) {
    case caseOne:
        // Code Block
        break;
    case caseTwo:
        // Code Block
        break;
    case caseThree:
        // Code Block
        break;
    default:
        // Code Block
}
```

**Ternary Operator**

```java
int num = (condition) ? expressionTrue : expressionFalse;
```

### Loops

**For**

```java
for (int i = 0; i < nums.length; i++) { /* Code */ }

// Enhanced For Loop
for (int num : nums) { /* Code */ }
```

**While**

```java
while (condition) { /* Code */ }
```

**Do While**

```java
do { 
    /* Code */
} while (condition);
```

## Exceptions

- Types of errors:
    - **Compilation errors** - detected by the compiler & prevent program compilation. e.g. syntax errors
    - **Run-time errors** (exceptions) - occur during program execution.
    - **Logical / semantic errors** - caused by incorrect logic.

```java
int a = 0;
int b = 0;

try {
    b = 10/0;
} catch(ArithmeticException e) {
    System.out.print("Can't Divide By Zero!");
} catch(AnotherSpecificException e) {
    System.out.print("A Specific Exception Occured!");
} catch(Exception e) {
    System.out.print("Something went wrong!");
}
```

- Only critical statements (statements likely to throw a run-time error) should be placed inside the `try` block of a `try`/`catch`.

- It's also possible to add an optional `finally` block.
    - Typically used for cleanup tasks, such as closing resources like files, database connections, or network sockets.
    - It is considered a good practice to use it when appropriate to ensure proper resource cleanup.
    - There can be only one `finally` block for each `try` block, but there can be multiple `catch` blocks.
    - The `finally` block will not be executed if the JVM exits while the `try` or `catch` code is being executed, such as when the `System.exit()` method is called.
- If the resources used in a `try` block implement the `AutoClosable` interface, try-with-resources feature can be used to automatically close the resources after the execution of the block. This removes the need for a `finally` block.
    - Multiple resources can be declared in a try-with-resources block by separating them with a semicolon inside `try()`.
    - Final & effectively final variables declared outside `try()` can be used inside a try-with-resources block.

```java
/* Try-Catch-Finally */
Scanner s = null;
try {
    s = new Scanner(new File("file.txt"));
    while (s.hasNext()) {
        System.out.print(s.nextLine());
    }
} catch (FileNotFoundException e) { /* Catch Block Code */ } 
finally {
    if (scanner != null) {
        scanner.close();
    }
}

/* Try-with-Resources */
try (Scanner s = new Scanner(new File("file.txt"))) {
    while (s.hasNext()) {
        System.out.print(s.nextLine());
    }
} catch (FileNotFoundException fnfe) { /* Catch Block Code */ }
```

- The `Exception` superclass is a member of `java.lang`.
    - Custom exceptions can be created by extending the `Exception` superclass.

```java
class MyException extends Exception {
    public MyException(String s) {
        super(s);
    }
}
```

> [!note] 
> `throw` can be used to throw an exception.

```java
int a = 0;
try {
    a = 0/10;
    
    if (a == 0) {
        throw new ArithmeticException("Quotient is Zero!");
    }
} catch (ArithmeticException e) {
    System.out.print(e);
}
```

### Checked Exceptions

- Checked by the compiler at compile-time.
- Handling these exceptions (using `try-catch` blocks) or declaring them in the method signature (using the `throws` clause) is required.
- Examples: `IOException`, `SQLException`, `ClassNotFoundException`, etc.

```java
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;

public class CheckedExceptions {
    public static void main(String[] args) {
        try {
            readFile("file.txt");
        } catch (FileNotFoundException e) {
            System.out.println("File Not Found: " + e.getMessage());
        } catch (IOException e) {
            System.out.println("IO Error: " + e.getMessage());
        }
    }

    public static void readFile(String fileName) throws FileNotFoundException, IOException {
        FileInputStream fis = new FileInputStream(fileName);
        // Do File Reading & Processing
        fis.close();
    }
}
```

### Unchecked Exceptions

- Are not checked by the compiler at compile-time.
- Handling these exceptions or declaring them in the method signature is not required.
- Examples: `NullPointerException`, `ArrayIndexOutOfBoundsException`, `IllegalArgumentException`, `RuntimeException`, etc.

```java
public class UncheckedExceptions {
    public static void main(String[] args) {
        int[] numbers = {1, 2, 3};
        
        try {
            int result = divideByZero(10, 0);
            System.out.println("Result: " + result);
            
            // ArrayIndexOutOfBoundsException
            int value = numbers[3]; 
        } catch (ArithmeticException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }

    public static int divideByZero(int a, int b) {
        // ArithmeticException
        return a / b; 
    }
}
```

### `Error`

- Represents a serious problem that the application should not try to handle, such as `OutOfMemoryError` or `StackOverflowError`. 
- Typically not handled by the application but rather by the JVM.

### `throws`

- Used in the method signature to declare that a method can throw one or more exceptions. 
- Specifies the type of exceptions that a method might throw during its execution.
- The responsibility of exception handling is passed onto the calling method.
    - The method that calls a method which `throws` an exception must either 
        - handle the exception using a `try-catch` block, or 
        - declare that it `throws` the exception as well.

```java
public static void readFile(String fileName) throws FileNotFoundException {
    FileReader reader = new FileReader(fileName);
}

public static void main(String[] args) {
    try {
        readFile("file.txt");
    } catch (FileNotFoundException e) {
        System.out.println("Exception caught: " + e.getMessage());
    }
}
```

## JVM

- The JVM is the core of the Java ecosystem, enabling Java-based software programs to run on any machine that has a JVM installed. 
- The JVM creates an isolated space on a host machine, allowing Java programs to execute regardless of the platform or operating system of the machine, which is a key feature that supports the "write once, run anywhere" approach.
- Java code is first compiled into bytecode, which is then interpreted by the JVM on the target machine. This allows Java programs to be platform-independent.

### Architecture

- **Class Loader** is responsible for loading Java classes into the JVM. 
    - It reads the bytecode files (.class files), verifies them, and loads them into the JVM.
- **Runtime Data Areas** are the memory areas allocated by the JVM for the execution of Java programs. 
    - Key areas include the heap (for dynamic memory allocation), the method area (for storing class and method data), and the stack (for storing local variables and partial results).
- **Execution Engine** executes the bytecode. It can use an interpreter or a [[Just-In-Time Compilation|Just-In-Time]] (JIT) compiler to convert bytecode into machine language instructions for execution. 
    - The JIT compiler improves performance by compiling bytecode into native machine code at runtime.
        - **Heap** is a region of memory used for dynamic memory allocation. 
            - It is where objects are allocated and deallocated.
        - **Stack** contains frames, each of which corresponds to a method invocation.
            - It stores local variables and partial results.
        - **Method Area** is where the JVM stores class and method data, including the runtime constant pool, field and method data, and the code for methods and constructors.
- **Native Method Interface (JNI)** allows Java code to call and be called by native applications and libraries written in other languages such as C, C++, and assembly.

## I/O

- I/O Streams represent an input source and an output destination.
    - **Input Streams** - used to read data from a source, one item at a time.
    - **Output Streams** - used to write data to a destination, one item at a time.
    - e.g. `InputStream`, `OutputStream`, `Reader`, `Writer`

- **Byte Streams** - used to read and write a single byte (8 bits) of data.
    - Derived from the abstract classes `InputStream` and `OutputStream`.
- **Character Streams** - used to read and write a single character of data.
    - Derived from the abstract classes `Reader` and `Writer`.

### File I/O

- `java.io` package provides classes for file I/O operations.
    - Examples: `FileInputStream`, `FileOutputStream`, `FileReader`, and `FileWriter`.
        - `FileReader` - used to read character data from a file.
        - `FileWriter` - used to write character data to a file.

**FileWriter** & **FileReader**

```java
// FileWriter
FileWriter writer = new FileWriter("output.txt");
writer.write("Hello, World!");
writer.close();

// FileReader
FileReader reader = new FileReader("input.txt");
int c;
while ((c = reader.read()) != -1) {
    System.out.print((char) c);
}
reader.close();
```

**Buffered Streams**

```java
import java.io.BufferedWriter;
import java.io.BufferedReader;

try {
    BufferedWriter writer = new BufferedWriter(new FileWriter("output.txt"));
    writer.write("Hello, Java.");
    writer.write("\nKeep Coding!");
} catch (IOException e) { /*...*/ }
finally {
    writer.close();
}


try {
    BufferedReader reader = new BufferedReader(new FileReader("output.txt"));
    String line;

    while((line = reader.readLine()) != null)
        System.out.println(line)
    
    reader.readLine();
} catch (IOException e) { /*...*/ }
finally {
    reader.close();
}
```

### Serialization

- Converting an object into a stream of bytes to store the object or transmit it over a network.
- Deserialization is converting the stream of bytes back into an object.
- The `java.io.Serializable` interface is used to mark a class as serializable.
- The `ObjectOutputStream` and `ObjectInputStream` classes are used to perform serialization and deserialization, respectively.

### User Input

**BufferedReader** 

```java
import java.io.BufferedReader;

System.out.println("Enter your age: ");

InputStreamReader in = new InputStreamReader(System.in);
BufferedReader bf = new BufferedReader(in);

int age = Integer.parseInt(bf.readLine());
System.out.println(age);

bf.close();
```

**Scanner**

```java
import java.util.Scanner;

Scanner scanner = new Scanner(System.in);
System.out.println("Enter your name: ");

String name = scanner.nextLine();
System.out.println("Hello, " + name);

System.out.println("How old are you?");
int age = scanner.nextInt();
System.out.println("You are " + age + " years old.");
```

## Packages

- A package is a directory structure for grouping classes together.

```java
package myJavaApp;
```

- When publishing a Java project to the public, it's must have a unique package name for imports. A common approach is to use a project's domain in reverse.

```java
package com.myJavaApp;
```

- `java.lang` is a core package that provides fundamental classes and features of the Java language.
    - e.g. `String`, `Integer`, `Object`
    - Classes in `java.lang` are auto-imported in every program.
- `java.util` is a utility package that provides a wide range of useful classes and features for more advanced programming tasks.
    - e.g. `ArrayList`, `HashMap`, `Scanner`
    - Classes in `java.util` need to be explicitly imported.

### Useful Packages

- `Random` class from `java.util.Random` and `Math.random()` from `java.lang.Math` can be used for generating random values.
- `java.time` (introduced in Java 8) contains classes to work with date/time.
    - `java.time.LocalDate` - date without a time-zone
    - `java.time.LocalDateTime` - date-time without a time-zone

### Imports

```java
import java.util.Date;
// import java.sql.Date; // Duplicate import not allowed ⛔

public class Main {
    public static void main(String[] args) {
        Date date = new Date();

        // Explicit class usage
        java.sql.Date dateSql = new java.sql.Date();
    }
}
```

> [!note]
> Using `*` imports all files in a package, not folders.
> 
> ```java
> import java.lang.*;
> ```

## OOP

- [[Object-Oriented Programming]] 📄

### Classes

```java
// Person.java
class Person {
    // Instance Variables
    String firstName;
    String lastName;
    boolean isAdult;

    // Static Variable
    static String role;

    // Constructor
    Person(String fName, String lName, boolean isAdult) {
        this.firstName = fName;
        this.lastName = lName;
        this.isAdult = isAdult;
    }

    // Method
    public void greet() {
        System.out.print("Hello, my name is " + this.firstName + ".");
    }
}
```

```java
// Main.java
public class Main {
    public static void main(String[] args) {
        Person john = new Person("John", "Doe", true);
        Person.role = "USER";
    }
}
```

> [!important]
> - There can be only one public class per source code file.
> 
> - If there is a public class in a file, the name of the file must match the name of the public class. For example, a class declared as `public class Person { }` must be in a source code file named Person.java.

> [!note]
> - The `new` keyword is required to dynamically allocate memory for objects at runtime. It is used to create instances of both regular classes and array objects.
>  
> - The `this` keyword is not necessary to access properties and methods within a class as long as there are no naming conflicts.

#### Inner Class

- Inner classes are classes defined within another class. 
- The class that contains the inner class is called the outer class.
- Inner classes can be further divided into two types: 
    - Non-static (inner class)
        - Are associated with an *instance* of the outer class.
        - Can access all the static and non-static members (variables and methods) of the outer class, including private members.
            - This allows for better encapsulation and organization of related code.
        - To create an instance of an inner class, you need an instance of the outer class first.
    - Static (static nested class)
        - Are static members of the outer class.
        - Are not associated with an *instance* of the outer class.
        - Can only access static members of the outer class, including private static members. 
- Inner classes can also be defined within a method of the outer class. 
- These are called method-local inner classes and share the scope of the method.
    - They have access to the variables of the method, including local variables.

```java
class OuterClass {
    private int outerVar = 10;
    private static int outerStaticVar = 20;

    class InnerClass {
        public void accessOuterVariable() {
            System.out.println("Outer variable: " + outerVar);
        }
    }

    static class StaticNestedClass {
        public void accessOuterStaticVariable() {
            System.out.println("Outer variable: " + outerStaticVar);
        }
    }
    
    public void outerMethod() {
        int localVariable = 10;

        class MethodLocalInnerClass {
            public void accessLocalVariable() {
                System.out.println("Local variable: " + localVariable);
            }
        }

        MethodLocalInnerClass inner = new MethodLocalInnerClass();
        inner.accessLocalVariable();
    }
}

public class Main {
    public static void main(String[] args) {
        // Inner Class
        OuterClass outer = new OuterClass();
        OuterClass.InnerClass inner = outer.new InnerClass();
        inner.accessOuterVariable();

        // Static Nested Classes
        OuterClass.StaticNestedClass nestedObj = new OuterClass.StaticNestedClass();
        nestedObj.accessOuterStaticVariable();

        // Method-Local Inner Classes
        OuterClass outer = new OuterClass();
        outer.outerMethod();
    }
}
```

- Inner classes are typically useful for creating helper classes, implementing callbacks, and organizing related code within a larger class structure.

#### Anonymous Inner Class

- An inner class that is defined without a name. 
- Created when an object of the class is instantiated.
- Can be useful to create a single instance of a class that is modified such as overriding methods, without having to define a separate named class.
- Has some limitations compared to named classes:
    - Cannot have constructors.
    - Cannot have static members, except for static final constants.
    - Cannot access local variables in their enclosing scope unless those variables are final or effectively final.

```java
MyClass obj = new MyClass() {
    @Override
    public void greet() {
        System.out.println("Hello!");
    }
};
```

- In the above snippet, `MyClass` can be an interface, an abstract class, or a concrete class.

#### Immutable Classes

- Immutable classes are classes where the state of the object cannot be changed once it is created.

- Some examples of immutable classes:
    - `java.lang.String`
    - Wrapper classes like `Integer`, `Long`, `Double`, etc.
    - `java.math.BigInteger` and `java.math.BigDecimal`
    - Unmodifiable collections like `Collections.singletonMap()`
    - Java 8 Date Time API classes like `LocalDate`, `LocalTime`, etc.    
- Guidelines for creating immutable classes:
    - The class should be declared as final so it cannot be extended.
    - All fields should be private and final so they can only be initialized once. 
    - Setter methods shouldn't be provided to change the object state. 
    - Only getter methods should be provided that return copies of mutable fields to avoid direct access. 
    - A constructor should be used to initialize all the fields.
- Key benefits of immutable classes:
    - **Predictability** - The state of the object will never change
    - **Thread-safety** - Immutable objects are inherently thread-safe
    - **Cacheability** - Results can be cached since the state never changes
    - **Simplicity** - Immutable objects are simpler to construct, test, and use

### `this()` & `super()`

- By default, when instantiating an object of a subclass, both constructors of the subclass and the superclass are called.
- The `super()` is always executed first thing in a constructor and it calls the constructor of a super class (if one exists).
    - When called explicitly, `super()` calls the constructor of the super class whose parameters match to the ones passed to it.
- `this()` executes the constructor of the same class with matching parameter list (similar to `super()`.

```java
class X {
    public X () {
        System.out.print("Called from X");
    }
    public X (int n) {
        System.out.print("Called from X: " + n);
    }
}

class Y extends X {
    public Y () {
        System.out.print("Called from Y");
    }
    public Y (int n) {
        super(n);
        System.out.print("Called from Y: " + n);
    }
}
```

```java
Y point1 = new Y(); 
/*
Called from X
Called from Y
*/

Y point2 = new Y(5); 
/*
Called from X: 5
Called from Y: 5
*/
```

> [!important] 
> Every class in Java extends `Object`. That means it inherits methods defined on `Object` such as `toString()` (which is called when printing an instance of a class) and `equals()`.

### `static`

- The `static` keyword can be used to define [[static properties & methods]].
- To initialize static properties of a class, we can do so in a `static` block.

```java
class Person {
    /* ... */
    static String role;

    static {
        role = "USER";
    }

    public static void printRole() {
        System.out.print("Role: " + role);
    }

    /* ... */
}
```

### `final`

- can be used with a variable, a method or a class.
    - Marking a class `final` makes it so that it *can't be inherited*.
    - Marking a method `final` makes it so that it *can't be overridden*.
    - Marking a variable `final` makes it constant so that it *can't be reassigned*.
- Performing those tasks on `final` variables, methods and classes causes a compile-time error.
- The position of the `final` keyword does not matter with respect to access modifiers.

```java
public final class FinalClass { /*...*/ }
final public class FinalClass { /*...*/ }

public final void finalMethod() { /*...*/ }
final public void finalMethod() { /*...*/ }

public final int finalVar = 42;
final public int finalVar = 42;
```

### `abstract`

- An abstract method is a method that is declared without an implementation, using the `abstract` keyword. 
- Abstract classes provide a base class that can be extended by subclasses, allowing for code reuse and the enforcement of a common interface or behavior.
- If a class has any abstract methods, the class must be declared as abstract.
- Subclasses of an abstract class must either provide implementations for all abstract methods or be declared as abstract themselves.
- Abstract classes can have both abstract and non-abstract (concrete) methods. They can also have constructors, instance variables, and static methods.
- Since Abstract classes are meant to be extended, they cannot be `final`.
- Classes that have full implementation for all of their methods, including any abstract methods inherited from superclasses or interfaces are known as *concrete classes*.
    - Concrete classes can be instantiated directly using `new.

> [!important]
> Abstract classes cannot be instantiated directly, but they can be subclassed (extended).

```java
// Abstract Class
abstract class Vehicle {
    protected String model;

    public Vehicle(String model) {
        this.model = model;
    }

    public abstract double getFuelEfficiency();
}

// Concrete Class
class Car extends Vehicle {
    private double fuelEfficiency;

    public Car(String model, double fuelEfficiency) {
        super(model);
        this.fuelEfficiency = fuelEfficiency;
    }

    @Override
    public double getFuelEfficiency() {
        return fuelEfficiency;
    }
}

public class Main {
    public static void main(String[] args) {
        Car car = new Car("Camry", 45.6);

        System.out.println("Car fuel efficiency: " + car.getFuelEfficiency());
    }
}

```

### Abstract Classes vs. Interfaces

- Both cannot be instantiated.
- Abstract classes can have both abstract methods (without implementation) and concrete methods (with implementation), while interfaces can only have abstract methods (before Java 8), but since Java 8, they can also have default and static methods.
- Abstract classes can have instance variables and can have any access modifier, while Interfaces can only have static final variables (constants), which are implicitly public, static, and final.
- A class can extend only one abstract class, but it can implement multiple interfaces. Interfaces support multiple inheritance, while classes do not.
- Adding new methods to an abstract class can break existing subclasses, because they need to implement the new methods. Adding new methods to an interface (using default or static methods) maintains backward compatibility; Existing implementing classes do not need to be modified.
- Abstract classes are used when you want to provide some common functionality and state, and allow subclasses to extend and override the behavior. Interfaces are used to define a contract or a set of methods that a class must implement, without any implementation details.

### Anonymous Objects

- Anonymous objects are instances of a class that aren't assigned to a variable.

```java
new Person();

new Person("John").greet();
```

### Access Modifiers

#### Default Access

- If an access modifier isn't specified, the method's visibility is limited to the package it's defined in. 
    - This is more restrictive than `public`, but less restrictive than `private` or `protected`.
- The method will have the default "package-private", "private-protected" or "friendly" access level, which means the method is accessible within the same package (the package where the class is defined), but not from other packages, even if those packages contain subclasses of the class containing the method.

#### `public` 

- Makes members accessible from anywhere, both within the same package and from different packages. 
- Public classes, interfaces, and members form the public API of a library or application

#### `private` 

- Restricts access of members to only the class itself.
- This provides the highest level of encapsulation and data hiding.

#### `protected`

- Makes members accessible within the same package and to subclasses of the class in other packages.
- This is used to achieve inheritance across packages.

> [!note]
> - Access modifiers cannot be applied to local variables within methods, but they can be applied to classes, interfaces, variables, methods, and constructors. 
> 
> - In Java, it's not required to explicitly declare the access modifier of methods. 
> 
> - In general, it's considered good practice to explicitly specify the intended access level for methods (and other class members) using the appropriate access modifier keywords.
> 
> - The choice of access modifier depends on the level of encapsulation and accessibility required for a particular member. It's generally recommended to use the most restrictive access modifier that meets the requirements, following the principle of least privilege.

### Inheritance

- If an instance variable in a superclass has `public`, `protected`, or default (no modifier) access, a subclass can directly access and use that variable (without `this`).
- The `super` keyword can also be used to access instance variables of a superclass, even if they are hidden by variables with the same name in the subclass.

```java
class SuperClass {
    int x = 10;
}

class FirstSubClass extends SuperClass {
    void accessSuperClassVar() {
        System.out.println(x);
    }
}

class SecondSubClass extends SuperClass {
    // Hides variable from SuperClass
    int x = 20; 

    void printX() {
        System.out.println(x);        // Prints 20
        System.out.println(super.x);  // Prints 10
    }
}
```

- While it is possible to have an empty subclass in Java, it is not valid to have an empty subclass that extends a superclass with a default parameterized constructor and does not provide a constructor itself.

```java
class Car {
    protected String make;

    public Car(String make) {
        this.make = make;
    }
}

// ⛔
class Gasoline extends Car {
    // 'super()' called by default, but there is no 
    // constructor in Car matching its parameter signature
}

// ✅
class Gasoline extends Car {
    public Gasoline(String make) {
        super(make);
    }
}
```

#### Multiple Inheritance

- Java does not support [[multiple inheritance]] of classes. 
    - A class in Java cannot extend more than one class directly. 
    - This is to avoid [[the diamond problem]], where a subclass could inherit conflicting implementations of the same method from multiple parent classes. 
- However, Java supports multiple inheritance through interfaces. 
    - A class can implement multiple interfaces, effectively inheriting the methods declared in those interfaces.

```java
interface A {
    void method1();
}

interface B {
    void method2(); 
}

class C implements A, B {
    // Class C now has methods method1() and method2()
    // from interfaces A and B respectively
}

class C extends Z implements A, B { /*...*/ }
```

### Nested Classes

- A **nested class** or an **inner class** is a class that is a member of another class. 
- The class that contains the inner class is called the outer class. 
- There are several types of nested classes in Java:
    - **Non-static nested class** is not declared static. 
        - It has access to all members (fields, methods, etc.) of the outer class, including private members. 
        - It must be instantiated within an instance of the outer class.
    - **Static nested class** is declared with the `static` modifier. 
        - It does not have access to non-static members of the outer class. 
        - It can be instantiated without creating an instance of the outer class.
    - **Local class** is defined within a method.
        - Its scope is limited to the method in which it is defined.
    - **Anonymous class** is a special type of nested class that does not have a name.
        - It is defined and instantiated in the same expression.

```java
public class OuterClass {
    private int outerVariable = 5;

    // Non-static Nested Class
    class InnerClass {
        private int innerVariable = 10;

        public void accessOuterVariable() {
            System.out.println(outerVariable);
        }
    }

    // Static Nested Class
    static class StaticNestedClass {
        private static int staticNestedVariable = 15;

        public void accessStaticNestedVariable() {
            System.out.println(staticNestedVariable);
        }
    }

    // Local Inner Class
    public void methodWithInnerClass() {
        int localVariable = 20;

        class LocalInnerClass {
            public void accessLocalVariable() {
                System.out.println(localVariable);
            }
        }

        LocalInnerClass lic = new LocalInnerClass();
        lic.accessLocalVariable();
    }

    // Anonymous Inner Class
    public void useAnonymousInnerClass() {
        MyInterface obj = new MyInterface() {
            @Override
            public void doSomething() {
                System.out.println("Anonymous Inner Class in action!");
            }
        };
        obj.doSomething();
    }

    public static void main(String[] args) {
        // Accessing the Non-static Nested Class (Inner Class)
        OuterClass outerObj = new OuterClass();
        OuterClass.InnerClass innerObj = outerObj.new InnerClass();
        innerObj.accessOuterVariable();

        // Accessing the Static Nested Class
        OuterClass.StaticNestedClass staticNestedObj = new OuterClass.StaticNestedClass();
        staticNestedObj.accessStaticNestedVariable();

        // Accessing the Method-local Inner Class
        outerObj.methodWithInnerClass();

        // Accessing the Anonymous Inner Class
        outerObj.useAnonymousInnerClass();
    }

    interface MyInterface {
        void doSomething();
    }
}
```

## Functional Programming

- Java supports [[Functional Programming|FP]] concepts such as:
    - [[First-Class Functions]]
    - [[Pure Functions]]
    - [[Immutable|Immutability]]
    - [[Declarative Programming]]
    - Lazy Evaluation
    - [[Higher-Order Functions]]
    - [[Currying]]

```java
Function<Integer, Integer> cube = x -> x * x * x;

`Function<Integer, Function<Integer, Integer>> currySum = a -> b -> a + b;`
```

- A Consumer (`java.util.function.Consumer`) is a functional interface and it represents an operation that accepts a single input argument and returns no result. 
    - Useful to perform an operation on an input value, without the need to return anything.

```java
List<String> names = Arrays.asList("John", "Jane", "Bob", "Alice");

Consumer<String> consumer = new Consumer<>() {
    public void accept(String n) {
        System.out.println(n)
    }
};

names.forEach(consumer);
// OR simply
names.forEach(n -> System.out.println(n));
```

### Stream API

- Process collections of objects in functional style.
- Operate on a source such as a collection, array or I/O channel.

- A stream represents a sequence of elements that supports various methods to perform ops like filtering and mapping.
    - Can only be used once.
    - Allow method chaining (similar to array methods in [[JavaScript]])

```java
List<String> names = Arrays.asList("John", "Jane", "Bob", "Alice");
Stream<String> s = names.stream();

List<String> uppercaseNames = s
    .filter(name -> name.startsWith("J"))
    .map(String::toUpperCase)
    .collect(Collectors.toList());

System.out.print(uppercaseNames); 
// Output: [JOHN, JANE]
```

- Parallel streams can take advantage of multiple CPU cores to process data more efficiently.

```java
List<String> names = Arrays.asList("John", "Jane", "Bob", "Tim", "Megan", "Sam");

long count = names.parallelStream()
                   .filter(name -> name.length() > 3)
                   .count();

System.out.print(count); 
// Output: 6
```

- Commonly used Stream API methods:
    - `filter()`
    - `map()`
    - `reduce()`
    - `collect()`
    - `skip()`
    - `sum()`
    - `min()` and `max()`
    - `forEach()`
    - `sorted()`

## Generics

- Allow us to create classes that can accommodate different types.
- Don't work with primitive types. 

```java
class Printer<T> {
    T item;

    public Printer(T item) {
        this.item = item;
    }

    public void print() {
        System.out.print(item);
    }
}

Printer<Double> pi = new Printer<>(3.14);
pi.print();
```

- Generic methods work with any data type, even if the containing class is not generic.

```java
public class Utils {
    public static <T> void printArray(T[] array) {
        for (T element : array) {
            System.out.println(element);
        }
    }
    
    public static <K, V> void printKeyValuePair(K key, V value) { /*...*/ }
}

Integer[] intArray = {1, 2, 3, 4, 5};
Utils.<Integer>printArray(intArray);
```

- Generics can be bounded to a specific type or its subclasses using `extends`.
    - A generic type can extend a single class due to [[multiple inheritance]].
    - When extending a class and interfaces, the class must appear first.

```java
public class GenericClass <T extends MyClass & MyInterface> {}
```

```java
public static <T extends Number> double sum(List<T> numbers) {
    double total = 0.0;
    for (T number : numbers) {
        total += number.doubleValue();
    }
    return total;
}

List<Integer> intList = Arrays.asList(1, 2, 3, 4, 5);
double intSum = sum(intList);
```

- The wildcard (`?`) can be used to represent an unknown type in generics.
    - 3 main types:
        - **Upper Bounded Wildcards**: `? extends Type`
            - Allows any subtype of the specified type to be used.
            - e.g. `List<? extends Number>`
        - **Lower Bounded Wildcards**: `? super Type`
            - Allows any supertype of the specified type to be used.
            - e.g. `List<? super Integer>`
        - **Unbounded Wildcards**: `?`
            - Represents an unknown type, with no restrictions.
            - e.g. `List<?>` 
    - Guidelines for using wildcards:
        - Use `? extends Type` for "in" variables (input parameters).
        - Use `? super Type` for "out" variables (output parameters).
        - Use unbounded wildcards `?` when the code doesn't depend on the type parameter.

## Collection API

- The Java Collections Framework is a unified architecture for representing and manipulating collections in Java. 
- It provides a set of interfaces, implementation classes, and algorithms to work with collections of objects.

### `Collection`

- `Collection` is the root interface of the Java Collections Framework.
- Work with wrapper class types. 
    - e.g. `Integer`, `String`
- Implementations of the `java.util.Collection` interface:
    - `List`
        - `ArrayList`
        - `LinkedList`
    - `Queue`
        - `DeQueue`
    - `Set` - no indexes
        - `HashSet`
        - `LinkedHashSet`

- `Collections` is a utility class that provides static methods to operate on collections, such as sorting, searching, and synchronizing.

```java
List<Integer> arr = new ArrayList<>();

arr.add(1);
arr.add(2);
arr.add(3);

Collections.sort(arr);
```

- The `Comparator` interface is a functional interface that allows us to define custom sorting logic for objects.
    - It defines a single method `compare(T o1, T o2)` which must be implemented.

```java
class Person {
    String name;
    int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}

List<Person> people = new ArrayList<>();
people.add(new Person("Alice", 25));
people.add(new Person("Bob", 33));
people.add(new Person("Charlie", 28));

Comparator<Person> personComparator = (i, j) -> (i.age > j.age) ? 1 : -1;

Collections.sort(people, personComparator);
```

- `Comparable` is a functional interface that gives classes the ability to implement their own natural sorting logic. 
    - It defines a single method `compareTo(T o)` which must be implemented in the class.

```java
class Person implements Comparable<Person> {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public int compareTo(Person other) {
        return Integer.compare(this.age, other.age);
    }
}

List<Person> people = new ArrayList<>();
people.add(new Person("Alice", 25));
people.add(new Person("Bob", 33));
people.add(new Person("Charlie", 28));

Collections.sort(people);
```

- Collections implement `Iterator`.

```java
Iterator<Integer> values = arr.iterator();

while (values.hasNext())
    System.out.println(values.next());
```

### `Map`

- A set of key-value pairs.
    - `HashMap`
    - `Hashtable` - synchronized

```java
Map<String, Integer> pairs = new HashMap<>();

pairs.put("a", 1);
pairs.put("b", 2);
pairs.put("c", 3);

System.out.println(pairs);
System.out.println(pairs.get("a"));

for (String k : pairs.keySet()) {
    System.out.println(key + ": " + pairs.get(key));
}
```

## Lambda Expressions

- Concise way to represent anonymous functions.
- Consist of:
    - Zero or more parameters enclosed in parenthesis (which is optional for single parameter methods)
    - An arrow token (`->`)
    - A body (single expression or block of statements)
- Used to provide an implementation of a functional interface.
- Similar to [[JavaScript|JS]] arrow functions in use case and syntax.

```java
@FunctionalInterface
interface Calc {
    void add(int a, int b);
}

// Anonymous Inner Class
Calc c = new Calc() {
    @Override
    public void add(int a, int b) {
        System.out.println(a + b);
    }
};

// Lambda Expression
Calc c = (int a, int b) -> {
    System.out.println(a + b);
};
// OR
Calc c = (int a, int b) -> System.out.println(a + b);
// OR
Calc c = (a, b) -> System.out.println(a + b);
```

- `return` can be omitted when implementing non-void methods with single-line return statements.

```java
Calc c = (a, b) -> a + b;
```

## Threads

- Every thread must have a `run()` method.

```java
class A extends Thread {
    public void run() { /*...*/ }
}

class B extends Thread {
    public void run() { /*...*/ }
}

A a = new A();
B b = new B();

a.start();
b.start();
```

- `Thread` implements the `Runnable` interface, so it's possible to create and run threads by implementing `Runnable`.
    - Since extending multiple classes is not allowed, this is useful when the thread class needs extend another class.

```java
class A implements Runnable {
    public void run() { /*...*/ }
}

class B implements Runnable {
    public void run() { /*...*/ }
}

Runnable a = new A();
Runnable b = new B();

Thread t1 = new Thread(a);
Thread t2 = new Thread(b);

t1.start();
t2.start();
```

- Synchronization ensures thread safety by controlling access of multiple threads to shared resources.
    - `synchronized` can be applied to methods or blocks of code to prevent race conditions when using threads.
        - Synchronized methods and blocks of code can be `static`.
- Synchronization enables inter-thread communication using methods like `wait()`, `notify()`, and `notifyAll()`.

```java
class Counter {
    int count;

    // Synchronized Method
    public synchronized void increment() { count++; }

    public void decrement() {
        // Synchronized Block
        synchronized (this) {
            count--;
        }
    }
}

Counter c = new Counter();

Runnable a = () -> {
    for (int i = 0; i < 1000; i++) {
        c.increment();
    }
};
Runnable b = () -> {
    for (int i = 0; i < 1000; i++) {
        c.increment();
    }
};

Thread t1 = new Thread(a);
Thread t2 = new Thread(b);

t1.start();
t2.start();

t1.join();
t2.join();

System.out.print(c.count);
```

## Annotations

- A form of metadata that provide additional information about a program, but do not directly affect its execution. 
    - Used to provide supplemental information or instructions to the compiler, development tools, frameworks, or the JVM, and they can be applied to various program elements, including classes, interfaces, methods, fields, parameters, and local variables.
    - Start with the `@` symbol, followed by the annotation name and optional elements or values.
    - Widely used in various Java frameworks, libraries, and tools, such as JUnit for testing, Hibernate for [[ORM]], and [[Spring]] for dependency injection.
- While they do not change code behavior, but they can be processed and utilized by various tools and libraries.
    - They can be accessed and processed at runtime using reflection or annotation processors. 
- Java provides several built-in annotations, such as `@Override`, `@Deprecated`, `@SuppressWarnings`, and `@FunctionalInterface`.
- Can have elements (members) that can be assigned values when the annotation is used.
- Can be classified into different categories: 
    - Marker annotations - e.g. `@Override`
    - Single-value annotations
    - Full annotations
    - Type annotations
    - Repeating annotations
- Custom annotations can also be defined by creating an annotation type.

## Enumerations (Enums)

- A special data type in Java that represent a group of named constants.
    - The constants are typically named in uppercase letters.

```java
enum Shape { CIRCLE, SQUARE, RECTANGLE }
```

- Essentially a special class in Java that cannot be extended or inherited. 
    - They are implicitly `public`, `static`, and `final`.
- Commonly used to represent a fixed set of values, such as days of the week, months, directions, etc. 
    - They help ensure type safety and prevent invalid values.
- Can be used in `switch` statements, and the `values()` method can be used to iterate over all the enum constants.
- Values are zero-indexed, and their indexes can be accessed using the `ordinal()` method.

```java
enum Color { 
    RED, BLUE, GREEN;
}

Color c = Color.RED;
System.out.print(c.ordinal());  // 0
```

- Enums Can have their own methods, variables, and constructors, just like regular classes.

```java
enum EV { 
    RIVIAN(80000), LUCID(100000), TESLA;

    private int msrp;

    private EV() {
        this.msrp = 50000;
    }

    private EV(int msrp) {
        this.msrp = msrp;
    }

    public int getPrice() { /*...*/ }
    public void setPrice() { /*...*/ }
}

Color c = Color.RED;
System.out.print(c.ordinal());  // 0
```

## Regular Expressions

- Functionality provided through `java.util.regex`.

```java
import java.util.regex.*;

String emailRegex = "^[a-zA-Z0-9_+&*-]+(?:\\.[a-zA-Z0-9_+&*-]+)*@(?:[a-zA-Z0-9-]+\\.)+[a-zA-Z]{2,7}$";
String emailAddr = "example@example.com";

Pattern emailPattern = Pattern.compile(emailRegex);
Matcher emailMatcher = emailPattern.matcher(emailAddr);

if (emailMatcher.matches())
    System.out.println("Valid email address: " + email);
else
    System.out.println("Invalid email address: " + email);
```

## Best Practices

### Naming Conventions

- Variables and methods should start with a lowercase letter and be camel cased. 
- Constants should be defined in all uppercase letters.
- Classes and interfaces should start with a uppercase letter and be camel cased.

## New Features

### LVTI

- Local Variable [[Type Inference]]
    - `var` can be used to initialize a local variable.
    - Available since Java 10
    - It's not possible to use `var` on a variable without initializer.
    - `var` can be used as both a variable name and a keyword.

```java
var nums = new ArrayList();

int a; // Valid ✅
var b; // Invalid ⛔
```

### Records

- A concise way to define immutable data classes, reducing the boilerplate code typically required for classes that simply hold data (such as getters, setters, constructors, `equals()`, `hashCode()`, and `toString()`).
- Introduced in Java 14.
- Implicitly final and immutable by default.
    - All fields are `public`, `final`, and accessible via methods named after the fields.

```java
record Person(String name, int age) {
    public void greet() {
        System.out.print("Hi, my name is " + name + ".");
    }
}

/* ... */
Person person = new Person("John Doe", 33);

// Accessing record fields
System.out.println("Name: " + person.name());
System.out.println("Age: " + person.age());

// Calling a record method
person.greet();

// Printing the record
System.out.print("Person: " + person);
```
   
- Common methods like `equals()`, `hashCode()`, and `toString()` are automatically generated.
- Can have additional methods and constructors defined within the record body, allowing for custom behavior if needed.
- Useful for creating simple data carrier classes, also known as Plain Old Java Objects (POJOs) or Data Transfer Objects (DTOs), where the focus is on containing and transporting data rather than complex logic.

### Sealed Classes

## Keep Learning

- OOD
    - [OOD](https://www.coursera.org/learn/object-oriented-design)
    - [UML](https://www.youtube.com/watch?v=6XrL5jXmTwM)
- Serialization
- Networking & Sockets
- I/O 
    - Non-blocking I/O
- Custom Annotations
- JVM
    - Garbage Collection
        - https://www.youtube.com/watch?v=Mlbyft_MFYM
    - Memory Management
    - Class loading
    - Performance Tuning
    - JVM Arguments
- Concurrency / Threads 
    - Concurrency Utilities
    - Thread States
    - Multithreading
- Streams
    - https://youtu.be/2StXP1XaU04
- Effectively Final
- Sealed Classes
- Images
- Bit Manipulation
- Optionals
- Logging
    - Log4J

---
## Further

### Books 📚

- Effective Java (Joshua Bloch)

- The Well-Grounded Java Developer (Benjamin Evans)

### Learn 🧠

- [Java Full Course (Amigoscode - YouTube)](https://www.youtube.com/watch?v=Qgl81fPcLc8)

### Resources 🧩

- [Google Java Style Guide](https://google.github.io/styleguide/javaguide.html)

#### Learning

- [Amigoscode (YouTube)](https://www.youtube.com/@amigoscode/videos)

- [Coding with John (YouTube)](https://www.youtube.com/@CodingWithJohn/videos)

- [Marco Codes (YouTube)](https://www.youtube.com/@MarcoCodes/videos)

- [Visual Computer Science (YouTube)](https://www.youtube.com/@visualcomputerscience/videos)