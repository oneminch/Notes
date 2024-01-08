---
alias: Next
---
## Concepts

- What is Next.js
    - Layouts vs Templates
    - https://leerob.io/blog/using-nextjs
    - https://www.epicweb.dev/why-i-wont-use-nextjs
- Rendering
    - Prerendering
    - [Modern Rendering Patterns](https://www.lydiahallie.io/blog/rendering-patterns)
    - [Rendering on the Web](https://web.dev/rendering-on-the-web/)
    - Partial Prerendering
- Project structure
- Components: server and client
- Routing
    - Client-side navigation
    - Layouts
    - Dynamic routes
    - API routes
- Data fetching
    - server and client
        - server actions - https://www.youtube.com/watch?v=FKZAXFjxlJI
    - SSR, SSG, ISR
    - Streaming
    - Caching
- Server Actions
- Styling
- Assets & Optimization
- Metadata & SEO
- A11y
- Auth
    -  Auth0 - https://www.youtube.com/watch?v=yufqeJLP1rI
- Error Handling
- Testing
- State Managment
- v14
    - [Performance](https://youtube.com/watch?v=SqVLqvsiAYQ)
    - [Generative UI](https://youtube.com/watch?v=cIzsQBbZNxk)
    - [Next.js - React's Vision](https://youtube.com/watch?v=9CN9RCzznZc)
    - [Next.js 14](https://youtube.com/watch?v=gfU1iZnjRZM)

---

- Next.js provides a framework to structure React applications, and optimizations that improve the developer and user experience.
- Core features of Next.js:
    - File-based routing
    - Hybrid rendering
        - Using Middleware, we can run server-side code at the Edge.
    - Automatic code splitting
    - Support for different styling methods: CSS Modules, CSS-in-JS
    - API routes for server-side processing
    - Fast Refresh on development
    - Asset optimization
        - Automatic image optimization using the built-in `<Image>` component (from `next/image`)
    - SEO features
        - Customize metadata using the built-in `<Head>` component (from `next/head`)
    - Script optimizations
        - Using the built-in `<Script>` component (from `next/script`)
- Optimization features of Next.js:
    - Compiling
    - Minifying
    - Bundling
    - Code Splitting


```jsx
export default function App({ Component, pageProps }) {
  return <Component {...pageProps} />;
}
```

- Similar to `app.vue` in [[Vue.js|Vue]] / [[Nuxt.js]] applications, a default-exported `/pages/_app.js` is a top-level component that wraps all pages in a Next.js application. 
    - It can be used to keep state when navigating between pages, or to add global styles.

> [!important]
> Global CSS can only be imported inside `/pages/_app.js`.
## Rendering
### Pre-rendering

- Pre-rendering is the process of generating HTML for each page in advance. 
- HTML is displayed on initial load even if [[JavaScript|JS]] is disabled.
- It is followed by [[hydration]] to run JS code and make the page fully interactive.
- This improves [[Web Performance|performance]] and [[SEO]].
- Next.js pre-renders every page by default.
- There are 2 forms of pre-rendering: Static Generation & Server-side Rendering.
- Like in [[Nuxt.js]], Next.js lets you define any form of pre-rendering on per-page basis.
#### Static Generation

- [[Static Site Generators|Static Generation]] - generating HTML at ==build time==.
    - Can be done with or without data.
- `getStaticProps` is an `async` function exported alongside a page component that runs at build time in production. It can fetch external data, and send it as props to a page.
    - It can only be exported from a page.
    - In dev mode, it runs on every request.

> [!important]
> Because `getStaticProps` meant to be run at build time, data that’s only available during request time, such as query parameters or HTTP headers, are not accessible.

```js
export default function HomePage({ data }) { ... }

export async function getStaticProps() {
    const res = await fetch("https://api.example.com");
    const data = await res.json();
    
    return { props: { data } };
}
```
#### Server-side Rendering

- [[Server-side Rendering]] - generating HTML ==on demand== or ==on request time==.
    - Used in development mode.
- In similar fashion to `getStaticProps`, `getServerSideProps` is exported from a page and runs at request time.
    - It has a parameter (`context`) which contains request specific information.

```js
export async function getServerSideProps(context) {
    return {
        props: {
            // props for the page component
        },
    };
}
```
### Client-side Rendering

- It involves statically generating parts of a page that don't require data, and, after page load, fetch data on the client-side to populate the page with relevant data.
    - This approach can be useful for private or user-specific pages where SEO is irrelevant, such as dashboards.
- The [SWR](https://swr.vercel.app/) React hook can be a useful tool for client-side data fetching in Next.js
## Routing

- Next.js uses file-system routing.
- The built-in `<Link>` component (from `next/link`) enables client-side navigation between pages in the same Next.js app.
- A page is a React component exported from a file in the `pages/` directory.
### Types
#### Pages Router

- It uses the `pages/` directory.
    - Global layout: `pages/_app.jsx`
    - Entry point: `pages/index.jsx`
#### App Router

- App Router is a newer evolution of the Pages Router.
- It uses the `app/` directory.
    - Global layout: `app/layout.jsx`
    - Entry point: `app/page.jsx`
### Dynamic Routes

- In a statically generated Next.js app, when an `async` `getStaticPaths` is exported from a page that uses dynamic routes, Next.js will statically pre-render all the paths specified by the function.
- **Catch-all Routes**: `/pages/subroute/[...param].js`
    - Matches `/pages/posts/post-1`, `/pages/posts/post-1/subpost-1`, etc.
- **Custom 404 Pages**: `/pages/404.js`

```js
{/* /pages/posts/[slug].js */}
export default function Post() { ... }

// (1) SSR
export async function getServerSideProps(context) {
    const { query: { slug } } = context;
    // ...
}

// (2) SSG
// Return a list of possible values for 'slug'
export async function getStaticPaths() {
    return [
        {
            params: {
                slug: "...",
            }
        }, ...
    ];
}

// Fetch necessary data for a post using params.slug
export async function getStaticProps({ params }) { ... }
```
## API Routes

- API Routes are server endpoints created in the `pages/api` directory and defined as a [[Node|Node.js]] serverless functions. 
    - They can be dynamic just like page routes.

```js
export default function handler(req, res) { ... }
```

- A common use case for API routes is for handling forms.

> [!important]
> API Routes should *not* be fetched from `getStaticProps` or `getStaticPaths`.
## Styling

- Next.js supports different styling methods out of the box: Sass, CSS Modules, CSS-in-JS.
- Sass (`.scss` & `.sass`) imports are supported out of the box, including component-level Sass (`.module.scss` & `.module.sass`).
- Next.js compiles CSS using PostCSS, which can be configured using a top-level `postcss.config.js` file.
## Project Structure

- `app/`- app router
- `pages/`- pages router
- `public/` - storing static assets served from `/`
- `src/` - optional source directory





---

## Further

### Learn 🧠

- [Learn Next.js (by Next.js) ⭐](https://nextjs.org/learn)

- [Mastering Next.js (by Lee Robinson)](https://masteringnextjs.com/)

- [Next.js 13 (JavaScript Mastery) (YouTube)](https://www.youtube.com/watch?v=wm5gMKuwSYk)
### Videos 🎥

- [Getting Started with Next.js (Delba de Oliveira) (YouTube)](https://www.youtube.com/watch?v=OB-WaTs1KHY)
### Resources 🧩

- [unicodeveloper/awesome-nextjs](https://github.com/unicodeveloper/awesome-nextjs#readme)