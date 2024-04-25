## Concepts

- Fundamentals
    - Basic Syntax
    - Data Types + Variables
    - Control Flow - Conditionals, Loops
    - Functions
    - Exceptions
        - Checked
        - Unchecked
        - Errors
    - OOP
    - Packages
    - Collections - Data Structures
    - File I/O APIs
- JVM
- Garbage Collection
- Memory Management
- Tooling
    - Gradle
    - Maven
- Web Framework
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
- Advanced
    - Generics
    - Serialization
    - Streams
    - Threads
    - Networking & Sockets

---
- Java is a general-purpose, class-based, [[OOP]] language.
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
/* Entry Point of a Java Program */
class HelloWorld {
    public static void main(String[] args) {
        /* ... */
    }
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

### Type Casting / Conversion

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

### Type Promotion

```java
byte a = 10;
byte b = 20;

int c = a * b; // 200 (Outside byte range)
```


### Non-primitive Types / Reference Types

- Strings
- Arrays
- Classes
- Interface

> [!note]
> - Primitives are predefined in Java, while non-primitives are not (except for `String`).
>     - They are created by the developer.
> - Non-primitives have methods for performing certain operations, while primitives don't.
> - A primitive always has a value, while a non-primitive can be `null`.
> - A primitive type starts with a lowercase letter, while a non-primitive type starts with an uppercase letter.

## Operators

- **Arithmetic**: `+`, `-`, `/`, `*`, `%`

> [!note]
> [[Prefix vs. Postfix Increment|Prefix & postfix increment]] operations behave similarly to that of [[JavaScript]].

- **Comparison**: `<`, `<=`, `>`, `>=`, `==`, `!=`
- **Logical**: `&&`, `||`, `!`

## Control Flow

### Conditionals

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

#### Ternary Operator

```java
int num = (condition) ? expressionTrue : expressionFalse;
```

### Loops



## Packages

- A package is a directory structure for grouping classes together.


















---
## Further

### Learn 🧠

- [Java Full Course (Amigoscode - YouTube)](https://www.youtube.com/watch?v=Qgl81fPcLc8)