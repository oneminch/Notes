---
alias: TS
---

## Introduction

- TypeScript extends [[JavaScript]] with types.
    - is a superset of [[JavaScript]].
        - Any valid JS code is also valid TS code.
    - behaves like a [[compiled language]] with its compilation target being [[JavaScript|JS]].
    - is fully compatible with existing JavaScript code, which means you can use TypeScript in any JavaScript environment.
    - is a _[[Structural Type System|structurally typed type system]]_.
- TypeScript provides
    - Type Safety
    - Better Tooling Support
    - Improved Maintainability
    - Backwards Compatibility
- `tsc` is the CLI tool for TypeScript.

## Setup

- TypeScript can be added as a dev dependency to any existing project.
- `tsconfig.json` is used to customize the behavior of the TypeScript compiler.

```json
{
    "compilerOptions": {
        "target": "es5",
        "module": "commonjs",
        "strict": true,
        "outDir": "./dist",
        "rootDir": "./src"
    },
    "include": ["src"],
    "exclude": ["node_modules"]
}
```

- These options can also be used in the `tsc` command-line tool.

```bash
tsc --target ES5 --module commonjs
```

## Types

### Primitive Types

- `string`
- `number`, `bigint`
- `boolean`
- `undefined`
- `null`
- `void`
- `symbol`

### `object` Types

- Object types can either be anonymous, or be named using an interface and a type alias.

```ts
function printCoordinates(pt: { x: number; y?: number }) {
    console.log(`(x: ${pt.x}, y: ${pt.y})`)
}
```

> [!note]
> Optional properties have the possibility of becoming `undefined`, so it's important to check them before using them.

#### `type` aliases

- Instead of using object and union types directly in type annotations, we can use type aliases to provide a name for any type, and reuse them.

```ts
type Coord = number | string; 

type Point = {
    /** Attached Docs for Tooling */
    x: Coord; 
    y?: Coord;
}

function printCoordinates(pt: Point) {
    console.log(`(x: ${pt.x}, y: ${pt.y})`)
}
```

#### `interface`

- Another way to name an object type similar to a type alias.

```ts
interface User {
    username: string;
    isAdmin: boolean;
    subscribe(plan: string): string;
    // OR
    // subscribe: (plan: string) => string
}
```

- Any JS class created using `class` is also a valid interface.

> [!question] Interface vs. Type Alias
> - Unlike type aliases, interfaces support declaration merging. An interface can be defined multiple times and the compiler merges these definitions automatically into a single interface definition.
> 
> - Interfaces can also be extended either from `type` aliases or from another `interface`, and vice versa.
> 
> - Union types can't be extended by an interface.
> 
> - When extending types, duplicate property keys are merged into one with their types becoming a union type. 
> 
> - Interfaces don't allow duplicate keys.

```ts
// Declaration Merging
interface Coordinates2D {
    x: number
}

interface Coordinates2D {
    y: number
}

const coords: Coordinates2D = {
    x: 1,
    y: 5
}
```

```ts
// Extending
interface Coordinates2D {
    x: number
    y: number
}

interface Coordinates3D extends Coordinates2D {
    z: number
}

const coords3D: Coordinates3D = {
    x: 1,
    y: 5,
    z: 2
}

type User = { name: string }

// Interface extending a type
interface Admin extends User {
    extraPermissions: string[]
}

// Extending a type (using an intersection operator)
type Admin = User & { extraPermissions: string[] };

// Extending an interface (using an intersection operator)
type Coords3D = Coordinates2D & { z: number };
```

- ==Declaration merging== allows the compiler to merge two or more separate declarations declared with the same name into a single definition. The merged definition will have the features of all the original declarations.

```ts
class User {}

const aUser = new User()

// ⛔ greet is not available in 'User'
aUser.greet = function() => {}

/* ------------------------------ */

interface User {
    greet(): void
}

class User {}

const aUser = new User()

// ✅ greet is available from merged 'User' declaration
aUser.greet = function() => {}
```

> [!example] A Real-World Use Case of Declaration Merging
> Extending existing or third-party objects
> ```ts
> interface Window {
>     MY_GLOBAL_VAR: string;
> }
> 
> const myVar = window.MY_GLOBAL_VAR;
> ```

#### `Enums`

- Enum types are a set of named constants.
- They have a default numeric value or index that is zero-based and changes incrementally. The default numeric value can be changed by assigning the attribute to a number.

```ts
/*
enum UserResponse {
  No,   // Default - 0
  Yes,  // Default - 1
}
*/

enum UserResponse {
  No = 1,
  Yes,    // Value - 2
}

const choice = UserResponse.Yes;
```

- Values can also be strings or even a heterogenous mix (not recommended).

```ts
enum Choice {
    Yes = "YES",
    No = "NO",
}
```

#### `Tuples`

- Array-like types with specific number and order of elements.

```ts
type RGB = [number, number, number];

const white: RGB = [255, 255, 255];

type nameAgePair = [string, number];

const jane: nameAgePair = ["Jane Doe", 32];    // ✅
const john: nameAgePair = [32, "John Doe"];    // ⛔

// Read-only Tuples
const fn = (pair: readonly [string, number]) => { ... }
```

#### `Class`

```ts
class Point {
    x: number;
    y: number;

    move(x: number, y: number): void {
        this.x += x;
        this.y += y;
    }
}
```

#### `Array`

```ts
const fn = (arr: Array<number>) => { ... }

let arr: string[] = ["Hello", "TypeScript"]
```

> [!note]
> `ReadonlyArray` is a special type for arrays that shouldn’t be changed.
> e.g. `ReadonlyArray<T>`, `readonly T[]`
### More Types

#### Built-In Types

- `object` - any value that isn’t a primitive.
- `any` - used to avoid typechecking errors.
- `unknown` - the type-safe counterpart of `any`. 
    - It's not legal to perform any operations on an `unknown` value.
- `void` - the return value of functions which don’t return a value. 
    - It’s the inferred type of a function with no or empty `return` statements.
- `never` - the return type for a function expression that always throws an exception or never returns.

#### Combining Types

##### Union Types

- Used to declare any type from the types in a union.

```ts
let count: number | string = 30;

let list1: (string | number)[] = [1, 2, "3"];

let list2: string[] | number[] = [1, 2, 3];

let canVote: "yes" | "no";
canVote = "yes"     // ✅
canVote = "maybe"   // ⛔
```

> [!important]
> TypeScript will only allow a method on a value if it is valid for _every_ member of the union. For instance, a variable of type `string | number` can’t use methods that are only available on `string` such as `toLowerCase()`.

> [!note]
> Enums can be rewritten using union types.
##### Intersection Types

- Types can be 'extended' from other types or interfaces using an intersection operator (`&`).

```ts
type User = { name: string }

type Admin = User & { extraPermissions: string[] };
```

##### `keyof`

- The `keyof` operator produces a string or numeric literal union of the keys of an object type.

```ts
type UserAttributes = keyof User;

const getVal = (obj: User, prop: UserAttributes) => {
    return obj[prop]
}
```

##### `typeof`

- The `typeof` operator can be used to define dynamic types from another value when the initial structure is unknown.

```ts
const myType = { x1: 2, x2: 50 }

function map(src: typeof myType) { ... }
```

- To use the return type of a function as a type:

```ts
const fn = () => { ... }

type FnType = ReturnType<typeof fn>;

function anotherFn(data: FnType) { ... }
```

##### Indexed Access Types

- Types can be accessed used JS object bracket syntax.

```ts
type User = {
    id: string;
    name: string;
    age: number;
}

type UserId = User["id"];
```

##### Mapped Types

```ts
type User = {
    name: string;
    age: number;
}

type Subscriber<Type> = {
    [Prop in keyof Type]: (val: Type[Prop]) => void
}

type UserSub = Subscriber<User>
/*
type UserSub = {
    name: (val: string) => void
    age: (val: number) => void
}
*/
```

## Basic Usage

- Typechecking in `.js` files can be allowed by setting the `compilerOptions.allowJs` property to `true` and using JSDoc to declare types.

```js
/**
 *
 * @param {string} greeting
 * @param {string} name
 * @returns {string}
 */
export default function logGreeting(greeting, name) {
    return `${greeting}, ${name}!`;
}
```

- In `.ts` files, ==type annotations== can be used to explicitly specify the type of a variable.

```typescript
// Explicitly typed variables
let str1: string = "Hello, Typescript!"
let arr: number[] = [1, 2, 3]
// OR let arr: Array<number> = [1, 2, 3]
let rgbColors: number[][] = [
    [255, 0, 0],
    [0, 255, 0],
    [0, 0, 255],
]
```

- Wherever possible, TypeScript automatically _infers_ types of a value.

```typescript
// Implicitly typed variables
let str2 = "Hello, Typescript!"

// Loosely typed variables
let str3: any = "Hello, Typescript!"
```

### Functions

```typescript
// Typed functions & parameters
// void return type
function printError(err: string): void {
    console.error(err);
}

// object return type with optional properties (?)
function createUser(name: string, age?: number):{name: string, age: number} {
    return {
        name: name,
        age: age
    }
}

// Arrow functions with return type
const add = (a: number, b: number): number => {
    return a + b;
}

arr.map((item):string => item.toUpperCase());

// Union Types
function printId(id: number | string) {
  console.log(id.toUpperCase());
  // Error - operations must be valid on every type of the union
  // toUpperCase is valid just for string
}
```

```typescript
// Type Aliases
type identifier = number | string;

type User = {
    readonly id: string;
    name: string;
    age: number;
    subscribed: boolean
}

function createUser(user: User) { ... }
```

> [!note]
> `readonly` properties won't change any behavior during runtime. They are useful to signal intent during development.
> 
> They also work similar to variable declarations using `const`. A `readonly` array property can still have its elements updated e.g. using `push()`, but can't be reassigned.

```ts
type Users = {
    readonly names: string[];  // Read-only
    count?: number;            // Optional
}

type UserIds = {
    [ids: number]: string;     // Index Signatures
}

let users: Users = { names: ["Jane", "John"], count: 2 };

users.names.push("Bob");
users.count++;
// ["Jane", "John", "Bob"]
```

#### Function Overloading

- In TypeScript, multiple functions can be defined that using the same name but with different number and/or type of parameters. 
    - The correct function to call is determined based on the number, type, and order of the arguments passed to the function at runtime.

```ts
// Overload Signatures
function createDate(timestamp: number): Date;
function createDate(m: number, d: number, y: number): Date;
// Implementation Signature
function createDate(mOrTimestamp: number, d?: number, y?: number): Date {
    if (d !== undefined && y !== undefined) {
        return new Date(y, mOrTimestamp, d);
    } else {
        return new Date(mOrTimestamp);
    }
}
        
const d1 = createDate(12345678); // ✅
const d2 = createDate(5, 5, 5);  // ✅
const d3 = createDate(1, 3);     // ⛔ No overloads expecting 2 arguments
```

## Type Assertions

- A way to tell the TypeScript compiler to treat a value as a specific type, regardless of its inferred type. 
- They are a way of indicating that the developer knows more about the type than the compiler, thus providing a way to override the type inference performed by the compiler.
- It can be done in two ways: `<[type]>value` or `value as [type]`

```ts
// Inferred type may be HTMLElement
const myCanvas = document.getElementById("canvas") as HTMLCanvasElement;
// OR
const myCanvas = <HTMLCanvasElement>document.getElementById("canvas");
```

```ts
// const assertions

// Type '"hello"' (instead of 'string')
let x = <const>"hello";

// Type 'readonly [10, 20]'
let y = [10, 20] as const;
```

### Non-Null Assertion

- The non-null assertion operator (`!`) is a type assertion that tells the compiler that a value will never be null or undefined.

```ts
let userInput: string | null = null;

let userInputLength = userInput!.length;
```

## Generics

- Generics are a way to write code that can work with multiple types, instead of being constrained to a single type.

```ts
function getValue<T>(obj: T, prop: keyof T) {
    return obj[prop]
}
```

- Using generics, we can write reusable functions, and classes that take one or more type parameters to act as placeholders for the actual data types that will be used when the function, or class is used.

```ts
interface Point {
    x: number;
    y: number;
}

// Instead of writing this
function clone(src: Point): Point {
    return JSON.parse(JSON.stringify(src));
}

let pt1: Point = { x: 5, y: 7 };
let pt2 = clone(pt1);

// We can do this
function clone<T>(src: T): T {
    return JSON.parse(JSON.stringify(src));
}

let pt1: Point = { x: 5, y: 7 };
let pt2 = clone(pt1);
```

- We can declare multiple generic types as well, but they need to be explicitly annotated using `< >` syntax.

```ts
function clone<T1, T2>(src: T1): T2 {
    return JSON.parse(JSON.stringify(src));
}

let pt1: Point = { x: 5, y: 7 };
let pt2 = clone<Point, Point>(pt1);
```

## Type Compatibility

- TypeScript uses a [[structural type system]] to determine type compatibility.
- In TypeScript, two types are considered compatible if they have the same structure, regardless of name.

## Type Guards / Narrowing

- Type guards are useful for when our code does something different depending on the type of variable. 
- We can use `typeof`, `instanceof`, equality of values (using equality operators) and truthiness of values (using logical operators) to ensure we are performing the right actions on the right types.

```ts
const padRight = (padding: number | string, input: string) => {
    if (typeof padding === "number") {
        return input + " ".repeat(padding);
    }
    
    return input + padding;
}

const logDate = (x: Date | string) => {
    if (x instanceof Date) {
        console.log(x.toUTCString());
    } else {
        console.log(x.toUpperCase());
    }
}
```

## Utility Types

### Records

```ts
interface User {
    name: string;
    age: number;
}

let Users: Record<number, User> = {
    0: {
        name: "Jane Doe",
        age: 32
    },
    1: {
        name: "John Doe",
        age: 39
    }
}
```

## Ecosystem

- **DefinitelyTyped** is a repository that provides high quality TypeScript type definitions for libraries.

```bash
pnpm add -D @types/node
```

- **tRPC** is a tool for easily building & consuming fully typesafe APIs without schemas or code generation.

- **Zod** is a TypeScript-first schema declaration and validation library.

```ts
import { z } from "zod";

// create schemas
const strSchema = z.string();
const UserSchema = z.object({
    username: z.string(),
});

// parse
strSchema.parse("tuna");  // "tuna"
strSchema.parse(12);      // throws ZodError
UserSchema.parse({ username: "johndoe" });
```

---
## Keep Learning
### Type Guards: Type Predicates
### Classes
### Decorators
### Utility Types

- Partial
- Omit
- Required
- Pick
- Readonly
- NonNullable
- ReturnType
- InstanceType
- Awaited

### Advanced Types
#### Conditional Types
#### Literal Types
#### Template Literal Types
#### Recursive Types
### Modules

---
## Further

### Books 📚

- Effective TypeScript (Dan Vanderkam)

- Learning TypeScript (Josh Goldberg)

- Programming TypeScript (Boris Cherny)

- TypeScript Cookbook (Stefan Baumgartner)

### Learn 🧠

- [TypeHero](https://typehero.dev/explore)

### Resources 🧩

- [TypeScript: Cheat Sheets](https://www.typescriptlang.org/cheatsheets)

### Roadmaps 🗺

- [TypeScript Roadmap](https://roadmap.sh/typescript)