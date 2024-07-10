---
alias: HyperText Transfer Protocol
---

## Concepts

- Status Codes
- CORS
- WebSockets
- http/2
- Cookies
    - https://http.dev/cookies
    - https://www.educative.io/blog/http-cookies
    - https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies
    - https://www.youtube.com/watch?v=sovAIX4doOE

---

- HTTP is a technique of transmitting data in a particular format between a server (destination) and a client (source).
- Considered stateless i.e. once a request and response has completed, the server doesn't retain any data about the request. 
- Capable of transmitting hypermedia documents as well as hypertext documents.
- Composed of two parts:
    - **Request**
        - created by a client
        - contains the request method, the target URL, the HTTP version, optional information (headers), and a body (for some methods)
    - **Response**
        - created by a server
        - contains the HTTP version, a status code and message the reflects the request outcome, optional information (headers), and a body (for some methods)
- In a URL, using a _fragment identifier_ `#text` is like a bookmark on the page or resource allowing the browser to scroll or navigate to that specific location on a page; It's never sent to the server with the request.
- Semantic URLs use human-readable words.

## HTTP Methods

### GET

- Used to retrieve data at a specified resource.
- Considered a safe and idempotent method.

### POST

- Used to send data to a server to create or update a resource.
- Non-idempotent.

### PUT

- Used to send data to the API to update or create a resource.
- Idempotent i.e. unlike POST, calling the same PUT request multiple times will always produce the same result.

### PATCH

- Similar to POST & PUT
- Only partial modifications are applied to the resource.
- Non-idempotent.

### DELETE

- Used to delete the resource at the specified URL.

### HEAD

- Almost identical to GET, but without the response body.
- Useful to check what a GET request will return before actually making a GET request.

### OPTIONS

- Returns data describing what other methods and operations the server supports at the given URL.
- Good candidate to test for fatal API errors.

### TRACE

- Used to echo the received request back to the client, allowing the client to see what changes or additions have been made by intermediate servers.
- Used primarily for diagnostic purposes and is not commonly used in regular web development.

## Status Codes

- Help identify the cause of the problem when a web page doesn't load properly.
- A status consists of a numeric status code and an HTTP reason phrase.
    - e.g. `500: Internal Server Error`

- `100` – `199` 
    - Informational responses
- `200` – `299` 
    - Successful responses
- `300` – `399` 
    - Redirection messages
- `400` – `499` 
    - Client error responses
- `500` – `599` 
    - Server error responses

## Ports

- **HTTP** - 80
- **HTTPS** - 443

---
## Further

### Learn 🧠

- [HTTP Networking Course - freeCodeCamp](https://www.youtube.com/watch?v=2JYT5f2isg4)

### Videos 🎥

![HTTP Status Codes Explained In 5 Minutes (YouTube)](https://www.youtube.com/watch?v=qmpUfWN7hh4)
