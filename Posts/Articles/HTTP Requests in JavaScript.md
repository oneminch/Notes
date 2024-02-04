---
id: http-requests-in-javascript
title: HTTP Requests in JavaScript
description: How to Make HTTP Requests in JavaScript
tags:
  - javascript
  - web-apis
  - http-requests
image: /content/cover/http-requests-in-javascript.png
cover_image: https://raw.githubusercontent.com/oneminch/portfolio/main/public/content/cover/http-requests-in-javascript.png
canonical_url: https://oneminch.dev/blog/http-requests-in-javascript
published_on: "2023-10-24"
---

Making requests is the heart of the Internet. Whenever you are browsing the internet, all what you are doing is requesting information from servers, which are basically interconnected computers. It's the foundation of how websites work. A simple case is a person typing "www.duckduckgo.com" and getting the DuckDuckGo search page. A request is made to a web server, which then sends back the files for that page, which will be rendered in the browser as a web page. This is made possible by a protocol known as HTTP (HyperText Transfer Protocol). On MDN web docs, the HTTP protocol is described as:

> HTTP is a protocol which allows the fetching of resources, such as HTML documents. It is the foundation of any data exchange on the Web, and it is a client-server protocol, which means requests are initiated by the recipient, usually the Web browser. A complete document is reconstructed from the different sub-documents fetched, for instance text, layout description, images, videos, scripts, and more.

Requesting a resource from the client side uses this HTTP protocol, and these types of requests are known as **HTTP requests**. These requests are essential for any type of online activity performed on the web.

JavaScript has a set of great tools and methods that allow us to make HTTP requests to send or receive data from a certain server or endpoint. A couple of commonly used ways to make requests are **XMLHttpRequest** and **Fetch**.

## XMLHttpRequest (XHR)

**AJAX** stands for **A**synchronous **J**avaScript **A**nd **X**ML. Requests made are _asynchronous_, which means they don't interrupt the execution of other JavaScript code. In other words, JavaScript code besides the AJAX code doesn't have to wait for requests to finish being executed. It can execute simultaneously. The method that makes this possible is the `XMLHttpRequest()`. Despite the prefix _'XML'_, we can process any form of data for our requests.

The `XMLHttpRequest()` method works as a constructor for us to create an instance and call our AJAX requests on.

```javascript
const xhr = new XMLHttpRequest();
```

Our `xhr` object has a number of methods and properties that allow us to make different types of requests.

### Methods

#### xhr.open()

We can then use the `open()` method on our `xhr` object to initialize or configure a request. This method takes the following parameters:

1. Method: GET, POST, PUT or DELETE,
2. URL: Path to our resource,
3. Async: Boolean value (`true` or `false`); Optional & default value is `true`,
4. Username & Password — Optional; Credentials if authentication is needed.

It follows the syntax:

```javascript
xhr.open(Method, URL[, Async]);
```

#### xhr.send()

This method allows us to open and send our request. It takes an optional parameter that contains our request body, which is useful when making POST requests.

```javascript
xhr.send([body]);
```

#### xhr.setRequestHeader()

This method is used to set HTTP headers for our request, such as `Content-Type` & `Accept`. Similarly, we can use `xhr.getResponseHeader()` to get header values from our response.

```javascript
// Set header for request
xhr.setRequestHeader("Content-Type", "application/json");

// Get header for response
xhr.getResponseHeader("Content-Type");
```

#### xhr.abort()

This method is useful when we want to cancel a request. Imagine a scenario where a user wants to cancel a request because it's taking too long. `xhr.abort()` can be used to stop the request.

```javascript
xhr.abort();
```

### Properties

#### xhr.response

This value contains the response body we receive from our request. `xhr.responseText` is also a similar property, which is used if our response is in a string format.

```javascript
const res = xhr.response;
```

#### xhr.responseType

This is used to set the response type for our `xhr` object. It can be in any one of these formats:

- `text`/`""` - default value
- `json`
- `document`
- `blob`

```javascript
xhr.responseType = "json";
```

#### xhr.readyState

Our request changes states as it progresses, and the current state of our request can be accessed by this property. Its values range from 0 (initial state) to 4 (completed state). The event `onreadystatechange` can be used to detect whenever there is a change in state.

```javascript
xhr.onreadystatechange = function () {
  if (xhr.readyState == 1) {
    /* request opened */
  }
  if (xhr.readyState == 2) {
    /* headers received */
  }
  if (xhr.readyState == 3) {
    /* response loading */
  }
  if (xhr.readyState == 4) {
    /* request complete */
  }
};
```

### Events

#### xhr.onload

This event is fired when our request is successful and the result is sent back. This can also be computed with `xhr.onreadystatechange` when `xhr.readyState` is 4.

```javascript
xhr.onload = () => {
  // Code to run when results are ready
};
```

#### xhr.onerror

This event is invoked when there is an error in our request, which could be due to network error or invalid configuration of our request.

```javascript
xhr.onerror = () => {
  // Code to run when request has failed
};
```

#### xhr.onprogress

This event is called repeatedly while our request is processed. It can be used to figure out the loading progress of a download or even a page load to let the user know how far along their request has been processed. An **event** parameter can be passed to `xhr.onprogress` and it has properties `event.loaded` and `event.total`, which can be used to show the actual progress feedback.

```javascript
xhr.onprogress = (event) => {
  // Code to run while request is being processed
  console.log(`Loaded ${event.loaded} of ${event.total}`);
};
```

### Example

We are going to use a simple fake online REST API called [JSONPlaceholder](https://jsonplaceholder.typicode.com/) to make example requests. We will use it to request and submit fake [posts](https://jsonplaceholder.typicode.com/posts). According to the documentation for JSONPlaceholder, our path to the resource we want is `https://jsonplaceholder.typicode.com/<endpoint>`, and there are several endpoints to choose from. For this demo, we'll use 'posts' as our endpoint. For this certain endpoint, we are going to receive and submit to an array of posts which are enclosed in objects. We also want our request to be asynchronous.

**Method: GET** - is used to retrieve data.

```javascript
// Our path to the resource
let reqURL = "https://jsonplaceholder.typicode.com/posts";

// 1. CREATE OUR XHR OBJECT
const xhr = new XMLHttpRequest();

// 2. SET OUR RESPONSE TYPE
xhr.responseType = "json";

// 3. CONFIGURE OUR REQUEST
xhr.open("GET", reqURL, true);

// 4. SEND THE REQUEST
xhr.send();

// 5. DECLARE FUNCTIONS BASED ON EVENTS
xhr.onload = () => {
  const data = xhr.response;
  console.log(data);
};

xhr.onprogress = (event) => {
  console.log(`Loaded ${event.loaded} of ${event.total}`);
};

xhr.onerror = () => {
  console.log("Request failed!");
};
```

As an output, we get a list of objects in the form of an array.

```javascript
// An example object from the array we get
{
    id: 1,
    title: "sunt aut facere repellat provident occaecati excepturi",
    body: "quia et suscipit suscipit recusandae consequuntur expedita et cum reprehenderit ...",
    userId: 1
}
```

**Method: POST** - is used to send new or updated data to the specified resource.

```javascript
// Our path to the resource
let reqUrl = "https://jsonplaceholder.typicode.com/posts";

// 1. CREATE OUR XHR OBJECT
const xhr = new XMLHttpRequest();

// 2. Configure a `POST` request
xhr.open("POST", reqUrl);

// 3. Create a JSON 'post' object
const json_data = {
  title: "this is title",
  body: "this is body",
  userId: 1
};

// 4. Set the `Content-Type` header
xhr.setRequestHeader("Content-Type", "application/json");

// 5. Pass a string form of our
//    json_data object to `send()`
xhr.send(JSON.stringify(json_data));

// 6. DECLARE FUNCTIONS BASED ON EVENTS
xhr.onload = () => {
  const data = xhr.response;
  console.log(data);
};

xhr.onprogress = (event) => {
  console.log(`Uploaded ${event.loaded} of ${event.total}`);
};

xhr.onerror = () => {
  console.log("Request failed!");
};
```

Other than the couple of steps we have added, the general structure and process of making HTTP requests is very similar and perhaps even almost identical.

For our demo API, the object we 'posted' is not actually added to their database of posts. Since it is a fake API, the process is also faked, as the purpose of this code and the API is to demonstrate how requests work and to test code.

**Method: PUT** - is used to update or modify data at the specified path. This is almost identical to our POST method process. The only things that change are the path, the method name and the object we are updating. Other than these values, the rest is the same.

```javascript
// 1. Our path to the object we want to update
//    Notice the '/1' added to the end
let reqUrl = "https://jsonplaceholder.typicode.com/posts/1";

// Configure a `PUT` request
xhr.open('PUT', reqUrl);

// Create a JSON 'post' object
// We added 'id' so it can be used to
// update the entry with the specified id
const json_data = {
    id: 1
    title: 'this is updated title',
    body: 'this is updated body',
    userId: 1
};
```

**Method: DELETE** - is used to delete the specified resource. Based on the documentation for the API, we use a different path to our resource to target and delete an entry.

```javascript
// 1. Our path to the object we want to delete
//    Notice the '/1' added to the end
let reqUrl = "https://jsonplaceholder.typicode.com/posts/1";

// 2. CREATE OUR XHR OBJECT
const xhr = new XMLHttpRequest();

// 3. Configure a `DELETE` request
xhr.open("DELETE", reqUrl);

// 4. SEND THE REQUEST
xhr.send();
```

For real APIs, we can continue to create another GET request to verify that the data we wanted to delete is actually deleted. We can retrieve all the data and see if the object we sent a DELETE request on is in the database. If it's not, then the data is deleted.

## Fetch

Fetch is a promise-based web API. It is a modern alternative to XHR. I have explained in detail how the `fetch()` API works [here](https://oneminch.dev/blog/the-javascript-fetch-api/). But let's redo the previous requests using fetch and see the difference.

**Method: GET**

```javascript
let reqUrl = "https://jsonplaceholder.typicode.com/posts";

fetch(reqUrl)
  .then((res) => res.json())
  .then((data) => console.log(data))
  .catch((error) => console.log(error));
```

**Method: POST**

```javascript
fetch(reqUrl, {
  method: "POST",
  body: JSON.stringify({
    title: "this is title",
    body: "this is body",
    userId: 1
  }),
  headers: {
    "Content-type": "application/json"
  }
})
  .then((res) => res.json())
  .then((data) => console.log(data))
  .catch((error) => console.log(error));
```

**Method: PUT**

```javascript
// Our path to the object we want to update
let reqUrl = "https://jsonplaceholder.typicode.com/posts/1";

fetch(reqUrl, {
  method: "PUT",
  body: JSON.stringify({
    id: 1,
    title: "this is title",
    body: "this is body",
    userId: 1
  }),
  headers: {
    "Content-type": "application/json"
  }
})
  .then((res) => res.json())
  .then((data) => console.log(data))
  .catch((error) => console.log(error));
```

**Method: DELETE**

```javascript
// 1. Our path to the object we want to delete
let reqUrl = "https://jsonplaceholder.typicode.com/posts/1";

fetch(reqUrl, {
  method: "DELETE"
});
```

Fetch is a much cleaner and simpler way of doing what XHR allows us to do. Tracking progress is not yet supported in fetch. Due to that and many other reasons like browser support, XHR is still an important part of making requests.

There are also third-party tools such as `axios` and jQuery's `$.ajax()`. These utilize XHR and/or Fetch API under the hood to provide a much cleaner way of making requests for developers.

## Read More

- [An overview of HTTP by Mozilla](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview)

- [XMLHttpRequest by JavaScript.info](https://javascript.info/xmlhttprequest)

- [HTTP Request Methods by Mozilla](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)
