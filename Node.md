---
alias: Node.js
---
## Concepts

- https://roadmap.sh/nodejs

- [Node.js - Learn](https://nodejs.org/en/learn)

---

## What is Node.js?

- An asynchronous event-driven runtime environment.
- Allows [[JavaScript]] to be run outside the browser.
- Single-threaded
    - A Node.js app runs without creating a new thread for every request.
- Execution stops as soon as there is no more tasks left in the event loop.
    - `http.createServer()` event never finishes running by default.
    - The event loop is only used to determine what to do next when the execution of a task finishes. 
    - e.g. In the snippet below, the `while` loop is not interrupted by `setTimeout`, because the event loop is only checked for new tasks once an ongoing execution is complete.

```js
setTimeout(() => {
    console.log('Timeout')
}, 1000)

console.log("Enter Loop")

let i = 0
while(new Date().getTime() < start.getTime() + 4000) {
    i++
}
console.log("Exit Loop")

/*
Output:
Enter Loop
Exit Loop
Timeout
*/
```

- Non-blocking I/O model using the *event loop* (events and callbacks)
    - Code is not necessarily executed in the order that it is written.
    - Every I/O operation takes a callback. When performing I/O, control is passed back to the event loop. The callback will be run once the data from the I/O operation is available.

```js
fs.readFile('/path/to/file.txt', (err, data) => {
    console.log(data);
});
```

- Built on the V8 [[JavaScript|JS]] engine
- Ideal use-cases:
    - APIs utilizing databases
    - streaming data
    - real-time data transfer (e.g. chat apps)
    - server-side web apps
- Not ideal for server-side processing that's CPU-intensive (e.g. file conversion)
    - For a CPU-intensive workloads, the only approach is to either optimize the algorithm to use less CPU or to scale to multiple cores and machines to utilize more CPUs.
- By default, request data is transferred in chunks and needs to be parsed (Streams & Buffers)
    - Streams are an event-driven way to handle data in Node.js that arrives in chunks, rather than all at once.

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

const createPage = (text) => (`
  <html>
    <head>
      <title>Welcome to Node.js</title>
    </head>
    <body>
      <h1>${text}</h1>
    </body>
  </html>
`);

http.createServer((req, res) => {
    res.setHeader("Content-Type", "text/html");
    
    if (req.url === "/") {
        res.write(createPage("Hello, Node!"));
        return res.end();
    }
    
    res.write(createPage("404 - Not Found!"));
    res.end();
}).listen(2345);
```

### The JavaScript Module System

> [!cite]- JS Module System
> ![[JS Module System]]

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

### Timers

- `setTimeout` can be used to delay the execution of a function. With a timeout delay of `0`, the callback function of a `setTimeout` call will be executed as soon as possible, but after the current function execution.

```js
setTimeout(() => {
    console.log('After');
}, 0);

console.log('Before');

/* 
Logs:
    Before
    After
*/
```

- This can be useful to avoid blocking on CPU-intensive tasks. 
    - The callback function is added to the queue in the scheduler and other functions can be executed beforehand.
- `setTimeout` and `setInterval` are global functions available in Node.js thru the `timer` module; They don't require imports.
- Timer functions in Node.js implement a similar API as the ones provided by [[Web Browsers]] but use a different internal implementation that is built around the Node.js Event Loop.

### Event Emitters



## File System

- `fs` contains file system access methods such as `readFile()` & `readFileSync()`.

- Modules
    - `path`
    - `process.cwd()`
- `__dirname`
- `__filename`

## Express

> [!cite]- Express
> ![[Express]]

## Testing

### Unit Testing

> [!example] Example: Testing a Node server with Jest & Supertest
```js
// app.test.js
const request = require('supertest');

describe('Product API', () => {
    describe('GET /api/products', () => {
        it('should return all products', async () => {
            const res = await request(app).get('/api/products');
            expect(res.statusCode).toBe(200);
            expect(res.body.length).toBeGreaterThan(0);
            expect(res.body[0]).toHaveProperty('id');
            expect(res.body[0]).toHaveProperty('name');
            expect(res.body[0]).toHaveProperty('price');
        });
    });

    describe('GET /api/products/:id', () => {
        it('should return a product if valid id is passed', async () => {
            const res = await request(app).get('/api/products/1');
            expect(res.statusCode).toBe(200);
            expect(res.body).toHaveProperty('id', 1);
        });

        it('should return 404 if invalid id is passed', async () => {
            const res = await request(app).get('/api/products/9999');
            expect(res.statusCode).toBe(404);
        });
    });

    describe('PUT /api/products/:id', () => {
        it('should update an existing product', async () => {
            const res = await request(app)
                .put('/api/products/1')
                .send({
                    name: 'Updated Name',
                    price: 69.99
                });
            expect(res.statusCode).toBe(200);
            expect(res.body.name).toBe('Updated Name');
            expect(res.body.price).toBe(69.99);
        });
    });

    describe('DELETE /api/products/:id', () => {
        it('should delete an existing product', async () => {
            const res = await request(app).delete('/api/products/2');
            expect(res.statusCode).toBe(204);
        });

        it('should return 404 if product not found', async () => {
            const res = await request(app).delete('/api/products/9999');
            expect(res.statusCode).toBe(404);
        });
    });
});
```

### E2E Testing

```js
// app.test.js
const puppeteer = require('puppeteer');

let server;
let browser;

beforeAll((done) => {
    server = http.createServer(app);
    server.listen(3000, () => {
        console.log('Test server running on port 3000');
        done();
    });
});

afterAll((done) => {
    server.close(done);
});

beforeEach(async () => {
    browser = await puppeteer.launch();
});

afterEach(async () => {
    await browser.close();
});

test("should display 'Hello, Node!'", async () => {
    const page = await browser.newPage();
    await page.goto("http://localhost:3000");
    
    const content = await page.content();
    expect(content).toContain("Hello, world!");
});
```

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

## Miscellany

### Streams

- The `stream` module provides a set of classes for working with streaming data. It includes implementations of readable, writable, duplex, and transform streams.

---

## Skill Gap
 
- Event Emitters 
- File System
- Command Line Apps
- Environment Variables
    - `dotenv`
    - `process.env`
- Testing Web APIs
    - Mock Tests using MSW
- HTTP Servers
    - `http`
    - Fastify, Nest.js, Adonis.js
    - `axios`
- Auth
    - Auth.js / Passport.js
- Template Engines
    - `ejs`
    - `pug`
    - `marko`
- [[Databases]]
- Logging
    - Log: Winston
- Threads
- Streams

---
## Further

### Books 📚

- [Mixu's Node book](https://book.mixu.net/node/single.html)

### Ecosystem 🏵
#### Frameworks

- AdonisJS

- Express

- Koa

### Learn 🧠

- [Node.js, Express, MongoDB & More (Udemy)](https://www.udemy.com/course/nodejs-express-mongodb-bootcamp/)

- [Node.js - Learn](https://nodejs.org/en/learn)

- [The Complete Node.js Developer Course (Udemy)](https://www.udemy.com/course/the-complete-nodejs-developer-course-2/)

- [The Web Developer Bootcamp (Udemy)](https://www.udemy.com/course/the-web-developer-bootcamp/)

### Resources 🧩

- [sindresorhus/awesome-nodejs](https://github.com/sindresorhus/awesome-nodejs#readme)

### Roadmap 🗺

- [Node.js Roadmap](https://roadmap.sh/nodejs)

### Videos 🎥

![Testing Node Server with Jest and Supertest (YouTube)](https://www.youtube.com/watch?v=FKnzS_icp20)

![Node.js Architecture - I/O (YouTube)](https://www.youtube.com/watch?v=DaU1-XoANig)