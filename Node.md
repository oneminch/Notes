---
alias: Node.js
---
## Concepts

- Architecture: https://www.youtube.com/watch?v=DaU1-XoANig

## Introduction

- an asynchronous event-driven runtime environment
- runs [[JavaScript]] outside the browser.
- single-threaded
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

**Node.js vs. the Browser**

- A single language is used to on both the frontend and the backend, but the ecosystem is different.
- [[DOM]] objects such as `document` and `window` don't exist in Node.js.
- The browser doesn't have access to APIs like ones that allow filesystem access.
- Node.js allows you to control the environment it runs in like the version of Node.js used. In browsers, the option of choosing the browser environment visitors will used doesn't exist.
    - We can therefore use the latest supported [[JavaScript|JS]] syntax without worrying about compatibility.
- Node.js supports both CommonJS (`require()`/`module.exports`) and ES module systems (`import`/`export`), while the browser is still getting implementation of the ES modules standard (`import`/`export`).

## Modules

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
### Built-in Modules

- `os`
- `path`
- `process`
    - `process.exit()` - exit an event loop

```js
const server = http.createServer((req, res) => {
    console.log(req);
    process.exit();
})
```

- `global`
- custom modules

## Package Management

- npm
    - Scripts
    - Workspaces
    - local vs global installation
- npx

## Error Handling

- Call stack & stack trace
- Debugging: Debugger
- Errors
    - Types
    - Uncaught exceptions
    - Async errors

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