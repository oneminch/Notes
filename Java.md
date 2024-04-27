## Concepts

- Fundamentals
    - Functions
    - Exceptions
        - Checked
        - Unchecked
        - Errors
    - OOP
    - Packages
    - Collections - Data Structures
    - Generics
    - File I/O APIs, NIO
- JVM
- Garbage Collection
- Memory Management
- Tooling
    - Maven
    - Gradle
- Web
    - Servlets & JSP
    - Java EE / Jakarta EE
        - EJB, JPA, JMS
    - [[Spring]]
- ORMs
    - JPA
    - Spring Data JPA
    - Hibernate
- Logging
    - Log4J
- JDBC
- Testing
    - JUnit
    - JMeter
- Docker
- Advanced
    - Serialization
    - Lambda Expressions
    - Streams
    - Threads
    - Networking & Sockets
    - Functional Programming

### Core Java Concepts

- Object-Oriented Programming (OOP) principles: Inheritance, Polymorphism, Encapsulation, and Abstraction
- Java language fundamentals: Data types, control structures, exceptions, collections, generics, and lambda expressions
- Multithreading and concurrency
- Java Virtual Machine (JVM) internals: Memory management, class loading, and garbage collection

### Java Ecosystem

- Java Enterprise Edition (Java EE/Jakarta EE): Servlets, JSP, EJB, JMS, JPA/Hibernate, JDBC
- Spring Framework: Core, MVC, Data, Security, and other modules
- Build tools: Maven and Gradle
- Testing frameworks: JUnit
- Logging frameworks: Log4j
- Web services: REST, SOAP, and related technologies (JAX-RS, JAX-WS)
- Containerization and deployment: Docker, Kubernetes, and cloud platforms (AWS, Azure, GCP)

---

## Fundamentals

- Java is a general-purpose, class-based, [[Object-Oriented Programming]] language.
    - [[Compiled Language|Compiled]], 
    - [[Statically-Typed Language|Strongly Typed]],
    - Platform-independent
    - Multi-threaded
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

#### Type Casting / Conversion

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

### Non-primitive Types / Reference Types

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

> [!note]
> - Primitives are predefined in Java, while non-primitives are not (except for `String`).
>     - They are created by the developer.
> - Non-primitives have methods for performing certain operations, while primitives don't.
> - A primitive always has a value, while a non-primitive can be `null`.
> - A primitive type starts with a lowercase letter, while a non-primitive type starts with an uppercase letter.

#### Interface



## Operators

- **Arithmetic**: `+`, `-`, `/`, `*`, `%`, `++`, `--`

> [!note]
> [[Prefix vs. Postfix Increment|Prefix & postfix increment]] operations behave similarly to that of [[JavaScript]].

- **Comparison**: `<`, `<=`, `>`, `>=`, `==`, `!=`
- **Logical**: `&&`, `||`, `!`

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

- As with [[JavaScript|JS]], curly brackets are optional for single line expressions inside conditionals.

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

### I/O and NIO

**User Input**

```java
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

```java
package com.myJavaApp;
```

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

- Classes available from the `java.lang` package don't need to be imported. e.g. `String`, `Math.

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

> [!note]
> The `this` keyword is not necessary to access properties and methods within a class as long as there are no naming conflicts.

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

### Access Modifiers

#### Default Access

- If an access modifier isn't specified, the method's visibility is limited to the package it's defined in. 
    - This is more restrictive than `public`, but less restrictive than `private` or `protected`.
- The method will have the default "package-private" or "friendly" access level, which means the method is accessible within the same package (the package where the class is defined), but not from other packages, even if those packages contain subclasses of the class containing the method.

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

> [!important]
> - There can be only one public class per source code file.
> 
> - If there is a public class in a file, the name of the file must match the name of the public class. For example, a class declared as public class Person { } must be in a source code file named Person.java.













---
## Further

### Learn 🧠

- [Java Full Course (Amigoscode - YouTube)](https://www.youtube.com/watch?v=Qgl81fPcLc8)