- Unlike other web frameworks which focus on building web apps, Astro is an MPA framework designed for content-heavy websites.
- It takes advantage of [[Server-Side Rendering|SSR]] by default which helps tackle performance issues raised by SPAs.
- It is also UI library-agnostic; you can use the commonly used component languages, like React, Vue and Svelte, on top of the built-in `.astro` UI language.
## Islands

- Another major aspect of Astro is its Island architecture. 

> An Astro Island is an interactive UI component on a static HTML page that always renders in isolation.

- To create an interactive UI component client-side [[JavaScript|JS]] is needed. 
- Islands allow the creation of such components in isolation without affecting the rest of the site. 
- Using a special `client` directive, we can explicitly state how and when to render each component.

---

## Further

### Learn 🧠

- [Astro Web Framework Crash Course (freeCodeCamp · YouTube)](https://www.youtube.com/watch?v=e-hTm5VmofI)

- [Astro Blog Course (Coding in Public · YouTube)](https://www.youtube.com/playlist?list=PLoqZcxvpWzzeRwF8TEpXHtO7KYY6cNJeF)