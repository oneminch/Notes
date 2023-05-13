## Introduction

- an asynchronous event-driven runtime environment
- runs [[JavaScript]] outside the browser.
- single-threaded
- non-blocking I/O model using the *event loop* (events and callbacks)
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

const page = `
  <html>
    <head>
      <title>Home</title>
    </head>
    <body>
      <h1>Hello!</h1>
    </body>
  </html>
`;

const srvr = http.createServer((req, res) => {
    console.log(req);

    res.setHeader("Content-Type", "text/html");
    res.write(page);
    res.end();
});

srvr.listen(2345);
```

**Built-in modules**
- `os`
- `path`
- `process`
    - `process.exit()`


- `global`
- custom modules

![[JS Modules]]

## Express

- utilizes middleware. 
    - incoming requests are automatically funneled thru functions processed on the way.
- abstracts away a lot of Node.js functionality.
- to be able to use multiple middleware functions, the `next()` function needs to be called at the end of each one.

```javascript
const express = require("express");

const app = express()

// Middleware
app.use((req, res, next) => {
    console.log("Middleware!");
    res.json({ name: "Dawit" });
    next();
});

app.use((req, res, next) => {
    console.log("Another Middleware!");
    res.send("<h1>Hello, Express!</h1>");
});

app.listen(3000);
```

- Express doesn't parse request body (`req.body`) by default. We can use parser packages like `body-parser` to achieve that.

```js
const bodyParser = require("body-parser");

// Parses form data
app.use(bodyParser.urlencoded({ extended: false }));

// We can now work with 'req.body'.
```

> [!note]
> To work with specific request methods, we can use `get()`, `post()`, `patch()`, `put()` and `delete()` instead of `use()`.

### Router

- It's considered good practice to make code modular. 
- Using routers in Express, we can define routes in separate route files and import them into our main file; as a convention a `~/routes/` directory is used to organize route logic.

```js
// ~/routes/admin.js
const express = require("express");

const router = express.Router();

// matches '/admin/add'
router.get("/add", (req, res, next) => {
    res.send(`
      <form action="/added" method="POST">
        <input type="text" name="user" >
        <button type="submit">submit</button>
      </form>
    `);
});

// matches '/admin/added'
router.post("/added", (req, res, next) => {
    console.log(req.body);
    res.redirect("/");
});

module.exports = router;
```

```js
// ~/app.js
const adminRoutes = require("./routes/admin");

// matches '/admin/*'
app.use("/admin", adminRoutes)
```

> The first argument of `app.use()` is an optional path value. By default, it's value is `/` which acts as a catch-all route. If another route middleware is needed it needs to precede the default catch-all route (`/`), and it shouldn't invoke the `next()` function.
> 
> We can also avoid this by matching exact paths using specific functions like `app.get()` & `app.post()`.
 
```javascript
// Should come first
app.use("/admin", adminRoutes);

// Exact match '/' route
app.get("/", (req, res, next) => {
    console.log("Middleware!");
});

// Catch-all route ('/*') for unhandled routes 
// Comes after all route handlers
// Can be used to render 404 pages
app.use("/", (req, res, next) => {
    res.status(404).send("<h1>Page Not Found!</h1>");
});
```

> [!note]
> `res` methods like `setHeader()` & `status()` can be chained together and must come before the `send()` method.

### MVC

![[MVC]]

#### Models

- How data is represented in the code.

### Views

- What the user sees and interacts with.
- Templates and [[HTML]] files to be rendered can be stored separately; as a convention a `~/views/` directory is used to organize such files.

```js
// ~/routes/home.js
const path = require("path");

router.get("/", (req, res, next) => {
    res.sendFile(path.join(__dirname, "..", "views", "index.html"));
});
```

- Alternatively, we can create a utility function to return the root directory of an application:

```js
// ~/utils/path.js
const path = require("path");

module.exports = path.dirname(require.main.filename);
```

```js
// ~/routes/home.js
const rootDir = require("../utils/path");

router.get("/", (req, res, next) => {
    res.sendFile(path.join(rootDir, "views", "index.html"));
});
```

> [!important]
> `path.join()` constructs an absolute path to the specified route that works on all operating systems. However, the path arguments passed are relative to the *current file* (`~/routes/home.js` above).

> [!note]
> Content that can be accessed publicly is stored in the `~/public` directory. It can be used to store static content like [[CSS]] files and static web files like [[robots.txt]].
> 
> e.g. If our stylesheet path is `~/public/css/style.css`, there needs to be extra configuration in Express to expose that file to the public: `app.use(express.static(path.join(rootDir, "public")))`. From HTML files, our stylesheet file can be accessed with `/css/style.css`.

#### Controllers

- The in-between logic connecting the models and views.
- Routes belong to this category.
- In the context of a Node/Express project, controllers might be split into different middleware functions.

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

## Command Line Apps

## Environment Variables

- `dotenv`
- `process.env`

## [[APIs]] 

### HTTP Servers

- `http`
- Express.js, Fastify, Nest.js
- `axios`

### Auth

- JWT
- Auth.js / Passport.js

## 

## Template Engines

- `ejs`
- `pug`
- `marko`

## Databases

- [[Databases]]

## Testing / Logging

- [[Software Testing]]
- Test: Jest / Mocha / Cypress
- Log: Winston

## Threads

## Streams


## Further

### Learn 🧠

- [Node.js, Express, MongoDB & More - Udemy](https://www.udemy.com/course/nodejs-express-mongodb-bootcamp/)

- [The Complete Node.js Developer Course - Udemy](https://www.udemy.com/course/the-complete-nodejs-developer-course-2/)

- [The Web Developer Bootcamp - Udemy](https://www.udemy.com/course/the-web-developer-bootcamp/)

### Roadmap 🗺

- [Node.js Roadmap](https://roadmap.sh/nodejs)