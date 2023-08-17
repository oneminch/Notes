---
alias: Nuxt.js
---
## Features

- Built on top of [Vue.js](Vue.js.md)
- File-system routing
- Automatic imports
- Multiple rendering modes:
    - [SSR](Server-Side%20Rendering.md)
    - [SSG](Static%20Site%20Generators.md)
    - Client-side only rendering
    - Hybrid rendering (Per route rules)
- Extensible using its module system

> [!info]
> Thanks to Nitro (the server engine that powers Nuxt 3) rendering can be done across different runtimes including the edge / workers.
## Commands

- `nuxi add` - adds a template of a file to a Nuxt project.

> [!example]
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
## Further

### Resources 🧩

- [Nuxt Docs](https://nuxt.com/docs)

- [nuxt-community/awesome-nuxt](https://github.com/nuxt-community/awesome-nuxt)