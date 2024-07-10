- A lightweight, interoperable and flexible web framework for Java and Kotlin. 
- Servlet-based.
- Supports modern features such as HTTP/2, WebSocket, and asynchronous requests.
- Considered as a library rather than a framework.
    - It sets no requirements for application structure.
    - There are no annotations, and no reflection.
- Supports OpenAPI.
- Runs on top of a fully configurable, embedded Jetty server.
    - If the embedded jetty-server is configured, Javalin will attach it’s own handlers to the end of the chain.

```java
import io.javalin.Javalin;

public class HelloWorld {
    public static void main(String[] args) {
        var app = Javalin.create(/*config*/)
            .get("/", ctx -> ctx.result("Hello, Javalin!"))
            .start(7070);
    }
}
```
