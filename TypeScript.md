- TypeScript extends [[JavaScript]] with types.
- It is a superset of [[JavaScript]].
- It behaves like a [[Compiled Language]] with its compilation target being [[JavaScript|JS]].
- A `tsconfig.json` file can be used to customize the behavior of the TypeScript compiler.

```typescript
// Explicitly typed variables
let str1: string = "Hello, Typescript!"
let arr: number[] = [1, 2, 3]

// Implicitly typed variables
let str2 = "Hello, Typescript!"

// Loosely typed variables
let str3: any = "Hello, Typescript!"
```