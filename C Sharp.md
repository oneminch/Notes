==???==
- StringBuilders - efficiency
- Function and constructor overloading
- DateTime / TimeSpan
- Enumerated types

---

- multi-paradigm, general purpose, [[Compiled Language|compiled]] [[high-level language]].

## Variables

```cs
var x = 5
```

## Data Types

- Get the data type of a value: `val.GetType()`
- All objects in .NET are descendants of `object`.

### Characters

```cs
char letter = 'a';  // single quoted
```

### String

```cs
string name = "Dawit";  // Double quoted

Console.WriteLine($"Hello, {name}!"); // String interpolation
```

- Common string properties & methods:
    - `str.Length`
    - `str.Replace(existingSubstring, newSubstring)`
    - `str.Contains()`
    - `str.IndexOf()`
    - `str.Insert(index, text)`
    - `str.Remove()`
    - `str.ToLower()` / `str.ToUpper()`
    - `str.StartsWith()` / `str.EndsWith()`
    - `str.PadLeft(num, str)` / `str.PadRight(num, str)`
    - `str.Trim()` / `str.TrimStart()` / `str.TrimEnd()` 
    - `String.Compare(str1, str2)`

> [!note]
> Prepending a string with `@` *ignores* escape characters. 
> 
> e.g. `Console.WriteLine(@"Hello!\n")` 

### Numbers

- `int` / `long` / `short`
- **Decimal**: `float` / `double` / `decimal`
    - `double` is the default floating point number.

```cs
int a = 3
int b = 2

var fp1 = 0.36f   // float
var fp2 = 0.36    // double
var fp3 = 0.36m   // decimal 
```

> [!info]
> In the above code block, the letters appended to the end of a number are called ==literal suffix==.

- **Range of `int`s**: `int.MinValue < x < int.MaxValue`
- `double`s represent double-precision floating point numbers.
    - **Range of `double`s**: `double.MinValue < x < double.MaxValue`
- `decimal`s have higher precision that `double`s but smaller range.
- When *overflow* or *underflow* happens during an integer operation, the result 'wraps around'. 

**Arithmetic Operators**: `+` / `-` / `*` / `/` / `%` (modulo)

- Integer division results in an integer value.
 
```cs
int a = 3
int b = 6
int c = (a + b)/2
// c = 4
```

### Boolean

- `bool`: `true` / `false`

**Comparison Operators**: `>`, `<`, `>=`, `<=`, `==`, `!=`
**Logical Operators**: `&&`, `||`, `!`

### Null

- A typed-variable can be set to null by appending `?` to the type of the variable declaration. 

```cs
int? num = null;
```

## Arrays, Lists & Collections

- Lists are a type of collection imported from `System.Collections.Generic` and are of the format `List<T>` where `T` is the data type of the items in the list. 
- Lists & arrays are zero-indexed, and can be accessed using bracket notation (similar to arrays in [[JavaScript]].

> [!note]
> Arrays in C# must be [[homogeneous]].

```cs
using System.Collections.Generic;

// Lists
var nums = new List<int> {1, 2, 3};


// Arrays
int[] favNums = new int[5];
string[] names = {"John Doe", "Jane Doe"};

// Heterogeneous arrays
object[] arr = {"A", 1, 3.14};

// Multi-dimensional arrays
string[,] multiDimArr = new string[2,3] { {"First Name", "Middle Name", "Last Name"}, {"Jane", "", "Doe"} };

Console.WriteLine(multiDimArr.GetValue(1,0));

int[,] numbers = { {1, 4, 2}, {3, 6, 8} };

foreach (int i in numbers) {
    Console.WriteLine(i);
}
// Or similarly
for (int i = 0; i < numbers.GetLength(0); i++) {
    for (int j = 0; j < numbers.GetLength(1); j++) { 
        Console.WriteLine(numbers[i, j]); 
    } 
} 
```

```cs
var nums = new[] {1, 2, 3};

int sum = 0;
foreach (var num in nums) {
    sum += num;
}
Console.WriteLine(sum);
```

```cs
// Custom lists
var List<Transaction> allTxns = new List<Transaction>();

// Dictionaries
var Mappings = new Dictionary<int, int>();
```

- Common array properties & methods:
    - `arr.Length`
    - `arr.SetValue(index, value)`
    - `Array.Copy(...)`
    - `Array.Sort(arr)`
    - `Array.Reverse(arr)`
    - `Array.Find(arr, condition)`
    - `Array.IndexOf(arr, item)`

- Common list properties & methods:
    - `listName.Count`
    - `listName.IndexOf(item)`
    - `listName.Add(item)` / `listName.Remove(item)`
    - `listName.Sort()` (In-place )

## Program Structure

```cs
using System;

namespace MyApp {
    class Program {
        // Program entry point
        static void Main(string[] args) {
            Console.WriteLine("Hello!");
        }    
    }
}
```

- `using` brings other libraries we can use in our code. e.g. `Console` class is part of `System`.

```cs
System.Console.Write("Hello!");

// OR

using System;

Console.Write("Hello!");
Console.WriteLine("Hello!");   // Adds newline after print
```

- `namespace` is used for organizing related classes. e.g. `System`

## Control Flow

### Loops

```cs
// while
while (condition) { /* ... */ }

// do...while
do {
    /* ... */
} while (condition);

// for
for (int index = 0; index < 10; index++) {
    /* ... */
}

// foreach
foreach (string name in names) { /* ... */ }
```

### Conditionals

### If / Else If / Else

```cs
if (condition1) {
    /* code block */
} else if (condition2) {
    /* code block */
} else {
    /* code block */
}
```

### Switch

```cs
switch(age) {
    case 1:
    case 2:
        // Code block
        break;
    case 3:
        // code block
        break;
    default:
        // code block
        break;
}
```

### Ternary Operator

```cs
int val = condition ? ifVal : elseVal;
```

## Type Casting

```cs
bool strToBool = bool.Parse("true");
int strToInt = int.Parse("100");
double strToDouble = double.Parse("3.14");

// Explicit conversion (data loss occurs)
int doubleToInt = (int)dblVal;

// Implicit conversion (no data loss)
long lngVal = intVal;
```

## Functions

```cs
// Function syntax template
<access specifier> <return type> <name>(Params)
{ <body> }

// Access specifier / modifier
// Is a function accessible from another class?
// public - yes
// private - yes
// protected - only from derived classes
```

**Default accessibility**

- Non-nested
    - class / constructor / delegate / interface - `internal`.
    - namespace / enum - `public`.
- Nested:
    - class methods & members - `private`.
    - members of a struct - `public`.

```cs
class Program {
    static double FindSum(double a = 1, double b = 1) {
        return a + b;
    }
    
    // Program entry point
    static void Main(string[] args) {
        double x = 12;
        double y = 5;
        Console.WriteLine($"{x} + {y} = {FindSum(x, y)}");
    }    
}
```

> [!note]
> - The `static` keyword in a function definition means it can be run without instantiating an object.

- [[Arguments]] of unknown type can be passed as `object`s.
    - e.g. `static void FuncName(object input) {}`
- Arguments are passed by value.
- To be able to pass by reference, the `ref` keyword can be used. 
    - e.g. `static void Func(ref int num) {}`
    - Similar functionality can be accomplished using `out`.

```cs
class Program {
    static void Swap(ref double a, ref double b) {
        double temp = a;
        a = b;
        b = temp;
    }
    
    // Program entry point
    static void Main(string[] args) {
        double x = 12;
        double y = 5;
        Console.WriteLine($"Before - x: {x}, y: {y}");
        Swap(ref x, ref y);
        Console.WriteLine($"After - x: {x}, y: {y}");
    } 
}
```

**[[Keyword Arguments]]**

```cs
static void Greet(string name, int age) { /* ... */ }

static void Main() {
    Greet(age: 34, name: "Jane Doe");
}
```


## OOP

- Classes are reference types, while structs are value types.

```cs
using System;

namespace MyApp {
    class Program {
        // Program entry point
        static void Main(string[] args) {
            User user = new User("Dan", 34, "Raleigh, NC");
            user.Greet();
        }    
    }

    class User {
        // Fields
        public string Name { get; }
        public int Age { get; }
        public string Location { get; }

        // Constructor
        public User(string name, int age, string location) {
            this.Name = name;
            this.Age = age;
            this.Location = location;
        }
        
        // Method
        public void Greet() {
            Console.WriteLine($"Hello, my name is {this.Name} and I'm a {this.Age} year old developer from {this.Location}.");
        }
    }
}
```

- `static` means a function can be run without instantiating an object. 

## Error Handling

```cs
if (condition) {
    throw new <ExceptionName()>;
}


try {
    var user1 = new User("John Doe ", 33, "NYC, NY, USA")
} catch (ExceptionName e) {
    Console.WriteLine(e.ToString())
}
```

## Further

### Learn 🧠

- [C#](https://invidious.snopyta.org/watch?v=M5ugY7fWydE&t=2h32m40s)

### Reads 📄

- [How to build a Serverless C# .Net Core API with a Database](https://softchris.github.io/pages/dotnet-serverless-database.html)
- [How to create a Serverless API in C# and .NET](https://softchris.github.io/pages/dotnet-serverless.html)

### Roadmaps 🗺

- [.NET Roadmap](https://raw.githubusercontent.com/Elfocrash/.NET-Backend-Developer-Roadmap/master/roadmap-dark-compact-2023.png)