- [Caching In: Defining, Optimizing, and Invalidating Your Cache](https://stack.convex.dev/caching-in)
- [Caching demystified: Inspect, clear, and disable caches #DevToolsTips - YouTube](https://www.youtube.com/watch?app=desktop&v=mSMb-aH6sUw)

- CDN
- cache-control
- Client-Side
- Server-Side
    - HTTP headers
    - Redis
    - Memcached

---

## `Cache-Control`

- An [[HTTP]] header that dictates how web content should be cached and managed by browsers and intermediary servers.
- Instructs browsers and other caching mechanisms on how to handle the caching of web resources. 
- **Primary Goals**:
    - Optimizing [[web performance]] by reducing unnecessary server requests
    - Ensuring content freshness
    - Balancing between serving up-to-date content and reducing server load
- **Directives**:
    - `no-store` - instructs that the response should not be stored in any cache. 
        - The most restrictive directive, often used for sensitive data.
    - `no-cache` - despite its name, this doesn't prevent caching. 
        - It requires the browser to revalidate the content with the server before serving it from the cache.
    - `max-age` - specifies how long (in seconds) a resource can be considered fresh before requiring revalidation.
    - `public` vs. `private`: 
        - `public`: - allows the response to be stored in shared caches.
        - `private` - restricts storage to private user caches only.

```javascript
app.use((req, res, next) => {
  res.set('Cache-Control', 'no-store');
  next();
});
```

> [!note] 
> While `Cache-Control` can significantly enhance web performance, it's crucial to balance performance gains with security considerations, especially for sensitive data.

- **Best Practices**
    - Use `no-store` for sensitive information.
    - Implement `max-age` strategically for static resources.
    - Consider using `must-revalidate` for critical resources.

---
## Further

### Reads 📄

- [All you (probably) need to know about caching on the web 🗃](https://dev.to/enterspeed/all-you-probably-need-to-know-about-caching-on-the-web-4loa)