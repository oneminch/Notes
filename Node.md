---
alias: Node.js
---
## Concepts

- Architecture: https://www.youtube.com/watch?v=DaU1-XoANig

## Introduction

- an asynchronous event-driven runtime environment
- runs [[JavaScript]] outside the browser.
- single-threaded
    - A Node.js app runs without creating a new thread for every request.
- non-blocking I/O model using the *event loop* (events and callbacks)
    - Code is not necessarily executed in the order that it is written.
- built on the V8 [[JavaScript|JS]] engine
- ideal use-cases:
    - APIs utilizing databases
    - streaming data
    - real-time data transfer (e.g. chat apps)
    - server-side web apps
- not ideal for server-side processing that's CPU-intensive (e.g. file conversion)
- by default, request data is transferred in chunks and needs to be parsed (Streams & Buffers)
- execution stops as soon as there is no more tasks left in the event loop.
    - `http.createServer()` event never finishes running by default.

> [!note]
> Due to non-blocking design of Node.js, code may not execute in the order it's written.

## Node.js vs. the Browser

- A single language is used to on both the frontend and the backend, but the ecosystem is different.
- [[DOM]] objects such as `document` and `window` don't exist in Node.js.
- The browser doesn't have access to APIs like ones that allow filesystem access.
- Node.js allows you to control the environment it runs in like the version of Node.js used. In browsers, the option of choosing the browser environment visitors will used doesn't exist.
    - We can therefore use the latest supported [[JavaScript|JS]] syntax without worrying about compatibility.
- Node.js supports both CommonJS (`require()`/`module.exports`) and ES module systems (`import`/`export`), while the browser is still getting implementation of the ES modules standard (`import`/`export`).

## Modules

### Built-in Modules

- Node.js provides a number of built-in modules that can be used without having to install them separately:

- `fs` provides an API for reading and writing files, as well as working with directories. 
    - It can be used to perform various file system operations such as creating, deleting, renaming, and modifying files.
- `path` provides utilities for working with file and directory paths.
    - It can be used to join multiple path segments together, resolve relative paths, and parse path strings into their components.
- `os` provides information about the operating system on which Node.js is running. 
    - It can be used to retrieve information such as the hostname, CPU architecture, and amount of free memory.
- `events` can be used to create custom events and handle them.
- `crypto` provides cryptographic functionality that can be used to generate hash values, encrypt and decrypt data, and generate random numbers.

- `http` & `https` modules allow us to launch a server among other things. 
    - `https` launches an SSL server.
    - Data send thru a `POST` request is sent as a stream which has to be buffered in to the desired data.

```js
const http = require("http");

const mainPage = `
  <html>
    <head>
      <title>Home</title>
    </head>
    <body>
      <h1>Hello!</h1>
    </body>
  </html>
`;

const errorPage = `
  <html>
    <head>
      <title>Home</title>
    </head>
    <body>
      <h1>404 - Not Found!</h1>
    </body>
  </html>
`;

const srvr = http.createServer((req, res) => {
    if (req.url === "/") {
        res.setHeader("Content-Type", "text/html");
        res.write(page);
        return res.end();
    }
    res.setHeader("Content-Type", "text/html");
    res.write(errorPage);
    res.end();
});

srvr.listen(2345);
```

### The JavaScript Module System

![[JS Module System]]

## Global Objects

### `global`

- In the browser, the top-level scope is understood to be the global scope, except within ES modules. 
    - Variables defined using `var` are created as members of the global object.
- In Node.js, the top-level scope is not the global scope. 
    - A variable declared in a module is local to that module, regardless of whether it is a CommonJS module or an ES module.

```js
var msg = "Hello, World!";

console.log(global.msg); // undefined
```

### `process`

- The `process` object provides information about and control over the current Node.js process. 
- It is a global object that can be accessed from anywhere in a Node.js application without requiring it.
- It offers various data sets about the program's runtime providing properties that allow for managing the Node.js process effectively like `process.versions`, `process.release`, and methods like `process.exit()` for exiting the event loop.
- Furthermore, it facilitates interactions with the environment through properties like `process.env` and enables access to command-line arguments via `process.argv`.

```js
const server = http.createServer((req, res) => {
    console.log(req);
    process.exit();
})
```

## Error Handling

- Call stack & stack trace
- Debugging: Debugger
- Errors
    - Types
    - Uncaught exceptions
    - Async errors

### Debugging

- `node --inspect`
    - enables inspector agent
    - listens on default address and port (127.0.0.1:9229)
- `node inspect script.js`
    - spawn child process to run script under `--inspect` flag
    - uses main process to run CLI debugger.

## Async Programming

- Synchronous code is said to be *blocking* can only execute after the one before has finished executed. e.g. `fs.readFileSync()` and `fs.writeFileSync()`

```js
const fs = require("fs");

const textIn = fs.readFileSync("input.md", "utf-8");
console.log(textIn);

const textOut = "Overwritten text.";
fs.writeFileSync("input.md", textOut);
```

- Node.js uses callbacks to make execution asynchronous / non-blocking. e.g. `fs.readFile()` and `fs.writeFile()`

```js
const fs = require("fs")

fs.readFile("input.md", "utf-8", (err, data) => {
    console.log(data)
});
console.log("Reading file...")
```

>[!note]
>Because of its event-driven architecture, some operations rely on callbacks that get executed during a certain event. The `return` keyword is often used before a function call to prevent further execution of code.

- Event emitter

## File System

- `fs` contains file system access methods such as `readFile()` & `readFileSync()`.

- Modules
    - `path`
    - `process.cwd()`
- `__dirname`
- `__filename`

## [[Express]]

## TypeScript

- Node.js doesn't have built-in TypeScript support. 
- `.ts` will have to compiled into `.js` files before running them with Node. 

```bash
npx tsc -p .
```

- During development, tools like `ts-node` can be used along with `nodemon` to automatically build and run TypeScript files.
- The Node.js ecosystem provides many TypeScript-first libraries and tools:
    - Prisma
    - NestJS
    - TypeORM
    - AdonisJS

## ---

### Command Line Apps

### Environment Variables

- `dotenv`
- `process.env`

### [[APIs]] 

### HTTP Servers

- `http`
- Express.js, Fastify, Nest.js
- `axios`

### Auth

- JWT
- Auth.js / Passport.js

### Template Engines

- `ejs`
- `pug`
- `marko`

### Databases

- [[Databases]]

### Testing / Logging

- [[Software Testing]]
- Test: Jest / Mocha / Cypress
- Log: Winston

### Threads

### Streams

The `stream` module provides a set of classes for working with streaming data. It includes implementations of readable, writable, duplex, and transform streams.

---
## Further

### Ecosystem 🏵
#### Frameworks

- AdonisJS

- Express

- Koa

### Learn 🧠

- [Node.js, Express, MongoDB & More - Udemy](https://www.udemy.com/course/nodejs-express-mongodb-bootcamp/)

- [The Complete Node.js Developer Course - Udemy](https://www.udemy.com/course/the-complete-nodejs-developer-course-2/)

- [The Web Developer Bootcamp - Udemy](https://www.udemy.com/course/the-web-developer-bootcamp/)

### Resources 🧩

- [sindresorhus/awesome-nodejs](https://github.com/sindresorhus/awesome-nodejs#readme)

### Roadmap 🗺

- [Node.js Roadmap](https://roadmap.sh/nodejs)