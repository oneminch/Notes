---
alias: Nuxt.js
---

> [!example]- Learning Roadmap
> - Server Components
>     - https://roe.dev/blog/nuxt-server-components/
> - APIs
>     - [Creating APIs in Nuxt with Daniel Roe - YouTube](https://www.youtube.com/watch?v=g6BVCBkRelw)
> - Islands
>     - https://nuxt.com/docs/api/components/nuxt-island
>     - https://masteringnuxt.com/blog/nuxt-islands
> - Rendering
>     - https://www.youtube.com/watch?v=CItLUDpMdrA
> - Design Patterns
>     - [Vue Patterns](https://www.patterns.dev/vue)
> - Testing
>     - [Nuxt 3 Unit Testing](https://www.youtube.com/playlist?list=PL9lzMEbdolKi-6O2DlUvZCJOvd9z7XEHg)
>     - https://masteringnuxt.com/blog/unit-testing-in-nuxt
> - Layers
>     - What problems does it solve?
>     - https://davestewart.co.uk/blog/nuxt-layers/
> - Auth
>     - https://masteringnuxt.com/blog/how-to-read-and-write-cookies-in-nuxt-3
>     - https://www.perplexity.ai/search/how-can-i-tfu.eY6uTdyRe.pLILaZzA
>     - https://www.vuemastery.com/blog/minimalist-nuxt-authentication/
> - Modules
>     - Scripts
>         - https://scripts.nuxt.com/docs/getting-started/confetti-tutorial

---
## Fundamentals

- Built on top of [Vue](Vue.md)
- File-system routing
- Automatic imports
- Multiple rendering modes:
    - [SSR](Server-Side%20Rendering.md)
    - [SSG](Static%20Site%20Generators.md)
    - Client-side only rendering
    - Hybrid rendering (Per route rules)
- Extensible using its module system

> [!info]
> Because of the server engine that powers Nuxt 3 (Nitro), rendering can be done across different runtimes including the edge / workers.

## CLI Snippets

- `nuxi add` - adds a template of a file to a Nuxt project.

> [!example]
> 
> ```bash
> # Generates `components/TheHeader.vue`
> nuxi add component TheHeader
> ```

- `nuxi build` - creates a `.output` directory with the application, server and dependencies ready for production.
- `nuxi dev` - start a dev server with HMR at `http://localhost:3000`.
- `nuxi generate` - pre-renders every route of an application and stores the result in plain [HTML](HTML.md) so that it can be deployed on any static hosting service. 
    - It triggers the `nuxi build` command with `prerender` set to `true`
- `nuxi init` - initializes a fresh Nuxt project.
- `nuxi preview` - starts a server to preview a Nuxt application generated after running the `build` command.

## Composables

- For performance reasons, composables such as `useFetch` should not be called inside functions or event handlers. It's recommended to call them only on the top-level.

### `useState`

- Nuxt provides an [[Server-Side Rendering|SSR]]-friendly state management composable,  `useState`.

```vue
<!-- SomeComponent.vue -->
<script setup>
const counter = useState('counter', () => 0)
</script>

<template>
    <div>
        <button @click="counter--">-</button>
        <span>{{ counter }}</span>
        <button @click="counter++">+</button>
    </div>
</template>
```

```vue
<!-- AnotherComponent.vue -->
<script setup>
const myCounter = useState('counter')
</script>

<template>
    <div>
        <button @click="myCounter--">-</button>
        <span>{{ myCounter }}</span>
        <button @click="myCounter++">+</button>
    </div>
</template>
```

## Modules

- Functions that sequentially run when starting Nuxt in development mode (`nuxi dev`) or building a project for production (`nuxi build`).

---
## Further
### Ecosystem 🌳

- Nuxt Content
- Nuxt Image
- Nuxt UI
- Sidebase

### Learn 🧠

- [Nuxt Modules: The Ultimate Guide (VueSchool.io)](https://vueschool.io/courses/nuxt-modules-the-ultimate-guide) ⭐

### Reads 📄

- [How to Upgrade to Nuxt 4](https://masteringnuxt.com/blog/complete-guide-how-to-upgrade-to-nuxt-4) ⭐

- [The Perfect Guide to Setting Up a New Nuxt Project (Estéban Soubiran)](https://soubiran.dev/posts/the-perfect-guide-to-setting-up-a-new-nuxt-project) ⭐

- [Understand Nuxt Hydration by Building useState From Scratch](https://masteringnuxt.com/blog/understand-nuxt-hydration-by-building-usestate-from-scratch)

- [Custom Error Pages in Nuxt 3](https://masteringnuxt.com/blog/custom-error-pages-in-nuxt3)

- [Nuxt Going Full-Stack: How to Validate Forms? (Estéban Soubiran)](https://soubiran.dev/posts/nuxt-going-full-stack-how-to-validate-forms)

- [Authentication in Nuxt 3 (DEV)](https://dev.to/rafaelmagalhaes/authentication-in-nuxt-3-375o)

### Resources 🧩

- [Alexander Lichter (YouTube)](https://www.youtube.com/@TheAlexLichter/videos) ⭐

- [nuxt/awesome](https://github.com/nuxt/awesome)

### Videos 🎥

![Server Components Keep Getting Better](https://www.youtube.com/watch?v=VyEPMQGozPk)

![You are using useFetch WRONG!  - Alex Lichter (YouTube)](https://www.youtube.com/watch?v=njsGVmcWviY)

![Nuxt Tips (Playlist)](https://www.youtube.com/watch?v=SXk-L19gTZk&list=PLQnM-cL9ttacXZavMQMT-0lyGki8iSkGF)

![Nuxt Performance In Depth (Alex Lichter - YouTube)](https://www.youtube.com/watch?v=laRJNkG_wls&list=PL06MUQt-_wls2sirXbt919cIbGvKv6k5Q&index=1)

![Nuxt 3 (Alex Lichter - YouTube)](https://www.youtube.com/watch?v=2tKOZc3Z1dk&list=PL06MUQt-_wlsRNxmbIvgVuhsXG_dN1XaO&index=1)

![Mastering Advanced Nuxt.js with Daniel Roe](https://www.youtube.com/watch?v=XnWXWye8sBM)

![Nuxt Nation 2024: Julien Huang - How to contribute to Nuxt - YouTube](https://www.youtube.com/watch?v=noy52jML_Ok)