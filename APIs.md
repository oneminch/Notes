## Concepts

- REST vs SOAP
- [[GraphQL]]
- gRPC
    - tRPC
- Open API Spec
- [Web API Design Series (YouTube)](https://www.youtube.com/playlist?list=PLP_rkG1reBjrCKy2Pb1bvjJKbKfantijk)
## Architectures

### SOAP

- Simple Object Access Protocol
- A protocol specification for exchanging structured information in the implementation of web services in computer networks.
- Use XML-based messages that follow a specific format.
- Ideal for enterprise applications
- An example request:

```
<soap:Envelope 
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:xsd="http://www.w3.org/2001/XMLSchema"
    xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
    <soap:Body>
        <GetUserInfo xmlns="http://example.com/">
            <userId>123</userId>
        </GetUserInfo>
    </soap:Body>
</soap:Envelope>
```

### RESTful

- Representational State Transfer
- Defines a set of constraints to be used for creating web services. 
- Use HTTP methods like GET, POST, PUT, and DELETE to perform operations on resources identified by URIs.
- Resource-based
- Ideal for web servers

```
GET /api/users/123
```

- A simple REST API in [[Express]]:

```js
let users = [
    { id: 1, name: "John Doe", email: "john@example.com" },
    { id: 2, name: "Jane Smith", email: "jane@example.com" },
];

// GET /users - Retrieve all users
app.get("/users", (req, res) => {
    res.json(users);
});

// GET /users/:id - Retrieve a specific user
app.get("/users/:id", (req, res) => {
    const user = users.find((u) => u.id === parseInt(req.params.id));
    
    if (!user) {
        return res.status(404).json({ error: "User not found" });
    }
    
    res.json(user);
});

// POST /users - Create a new user
app.post("/users", (req, res) => {
    const { name, email } = req.body;
    
    const newUser = { id: users.length + 1, name, email };
    users.push(newUser);
    
    res.status(201).json(newUser);
});

// PUT /users/:id - Update an existing user
app.put("/users/:id", (req, res) => {
    const { name, email } = req.body;
    
    const user = users.find((u) => u.id === parseInt(req.params.id));
    
    if (!user) {
        return res.status(404).json({ error: "User not found" });
    }
    
    user.name = name;
    user.email = email;
    
    res.json(user);
});

// DELETE /users/:id - Delete a user
app.delete("/users/:id", (req, res) => {
    const index = users.findIndex((u) => u.id === parseInt(req.params.id));
    
    if (index === -1) {
        return res.status(404).json({ error: "User not found" });
    }
    
    const deletedUser = users.splice(index, 1)[0];
    
    res.json(deletedUser);
});
```

### GraphQL

- A query language for APIs and a runtime for fulfilling those queries with existing data.
- Protocol-agnostic
- Reduce network load by giving clients the power to ask for exactly what they need.

```
query {
    user(id: "123") {
        name
        email
    }
}
```

### gRPC

- Google Remote Procedure Call
- High performance
- Ideal for microservices
- Use Protocol Buffers

### WebSockets

- Bi-directional communication
- Ideal for low-latency data exchange such as real-time / live collaboration applications

### Webhooks

- Asynchronous communication
- Ideal for event-driven applications

## OpenAPI Spec

- The OpenAPI Specification (OAS) is a community-driven open specification that provides a standard, language-agnostic interface to describe RESTful APIs. 
- It describes RESTful APIs in a machine-readable format, enabling a variety of tooling and automation around API development and consumption.
- It is maintained and developed by the OpenAPI Initiative under the Linux Foundation.
- Key points:
    - It defines a standard way to describe HTTP APIs, allowing both humans and machines to understand the capabilities of a service without additional documentation or inspection of network traffic.
    - It supports use cases such as interactive documentation, code generation for clients and servers, and automation of test cases facilitating both design-first and code-first API development approaches.
    - It is represented in either YAML or JSON formats and can be produced statically or generated dynamically from an application.

---
## Further

### Books 📚

- RESTful Web Services (Leonard Richardson & Sam Ruby)

### Learn 🧠

- [Web API Design Series (YouTube)](https://www.youtube.com/playlist?list=PLP_rkG1reBjrCKy2Pb1bvjJKbKfantijk)

### Reads 📄 

-  [Meet the Robowaiter APIs Serving Us Data](https://maggieappleton.com/api)

### Videos 🎥

![API Architecture Patterns](https://www.youtube.com/watch?v=4vLxWqE94l4)

![Build an API from Scratch with Node.js Express - Fireship](https://www.youtube.com/watch?v=-MTSQjw5DrM)

![REST vs GraphQL](https://www.youtube.com/watch?v=PTfZcN20fro)