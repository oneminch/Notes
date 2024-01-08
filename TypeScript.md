---
alias: TS
---
- TypeScript extends [[JavaScript]] with types.
- It is a superset of [[JavaScript]].
- It behaves like a [[compiled language]] with its compilation target being [[JavaScript|JS]].
- A `tsconfig.json` file can be used to customize the behavior of the TypeScript compiler.

## Basic Setup

- Installation
- Configuration
- Running

## Types

### Primitives

- `string`
- `number`
- `boolean`
- `void`
- `undefined`
- `null`

### Object Types

- `Class`
- `Arrays`

#### `Interface`

```ts
interface User {
    username: string,
    isAdmin: boolean,
    subscribe(plan: string): string
    // OR
    // subscribe: (plan: string) => string
}
```

- Unlike types, interfaces support declaration merging. An interface can be defined multiple times and the compiler merges these definitions automatically into a single interface definition.

```ts
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

- Interfaces can also be extended either from `type` aliases or from another `interface`, and vice versa.

```ts
interface Coordinates2D {
    x: number
    y: number
}

// Interface extending another interface
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

// Type extending a type (using an intersection operator)
type Admin = User & { extraPermissions: string[] };

// Type extending an interface (using an intersection operator)
type Coords3D = Coordinates2D & { z: number };
```

> [!note]
> Union types can't be extended by an interface.

> [!important]
> When extending types, duplicate property keys are merged into one with their types becoming a union type. 
> 
> Interfaces don't allow duplicate keys.

#### `Enums`

- Enum types have a default numeric value or index that is zero-based and changes incrementally. The default numeric value can be changed by assigning the attribute to a number.

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

#### `Tuples`

- Array-like types with specific number and order of elements.

```ts
type RGB = [number, number, number];

const white: RGB = [255, 255, 255];

type nameAgePair = [string, number];

const jane: nameAgePair = ["Jane Doe", 32];    // ✅
const john: nameAgePair = [32, "John Doe"];    // ⛔
```

### Other

- `any`
- `object`
- `unknown`
- `never`

### Combining Types

**Union Types**

```ts
let count: number | string = 30;

let list1: (string | number)[] = [1, 2, "3"];

let list2: string[] | number[] = [1, 2, 3];

let list3: (string | number)[] = [1, 2, "3"];

let canVote: "yes" | "no";
canVote = "yes"     // ✅
canVote = "maybe"   // ⛔
```

**Intersection Types**

- Types can be 'extended' using an intersection operator (`&`).

```ts
type User = { name: string }

type Admin = User & { extraPermissions: string[] };
```

- type aliases
- `keyof` operator

## Syntax

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

// Implicitly typed variables
let str2 = "Hello, Typescript!"

// Loosely typed variables
let str3: any = "Hello, Typescript!"

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
> `readonly` properties work similar to variable declarations using `const`. A `readonly` array property can still have its elements updated e.g. using `push()`, but can't be reassigned.

```ts
type Users = {
    readonly names: string[];
    count?: number;    // Optional
}

let users: Users = { names: ["Jane", "John"], count: 2 };

users.names.push("Bob");
users.count++;
// ["Jane", "John", "Bob"]
```


## Assertions

## Type Inference

## Type Compatibility

## Type Guards

## Functions

- Typing
- Overloading

## Types vs Interfaces

## Classes

## Generics

## Decorators

## Utility Types

## Modules


---
## Further

### Books 📚

- Effective TypeScript (Dan Vanderkam)

- Learning TypeScript (Josh Goldberg)

- Programming TypeScript (Boris Cherny)

- TypeScript Cookbook (Stefan Baumgartner)

### Learn 🧠

- [TypeHero](https://typehero.dev/explore)

### Roadmaps 🗺

- [TypeScript Roadmap](https://roadmap.sh/typescript)