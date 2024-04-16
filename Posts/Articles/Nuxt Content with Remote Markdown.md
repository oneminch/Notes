---
id: nuxt-content-with-remote-markdown
title: "Using Nuxt Content: Working with Remote Markdown Files"
description: "This post goes over how to get started with Nuxt Content to create a minimal blog, and how to work with remote markdown files."
tags: 
    - nuxt
    - nuxt-content
    - markdown
    - vue
    - github
image: "/content/cover/nuxt-content-with-remote-markdown.png"
cover_image: "https://raw.githubusercontent.com/oneminch/portfolio/main/public/content/cover/nuxt-content-with-remote-markdown.png"
canonical_url: "https://minch.dev/blog/nuxt-content-with-remote-markdown"
head:
  meta:
    - name: robots
      content: "index, follow"
    - name: author
      content: Dawit (@oneminch)
    - property: "og:type"
      content: article
    - name: "twitter:card"
      content: summary_large_image
published: true
published_on: "2024-04-15"
---

This article discusses how to get started with Nuxt Content to create a minimal blog, and how to work with remote Markdown files.

The first section goes over how to set up a project with Nuxt Content, and the second cover working with Markdown files. If you are already familiar with the setup steps, feel free to skip the first section.

## Get Started

### What is Nuxt?

[Nuxt](https://nuxt.com) is an open-source framework for building performant websites and full-stack applications using [Vue.js](https://vuejs.org/). It provides performance and SEO benefits, and adds full-stack capabilities for Vue apps. 

Nuxt is an appealing framework to work with, partly because of its robust module ecosystem. Popular UI libraries, headless CMS tools, and databases can be easily integrated with a single line of code. Among other third-party modules, [Nuxt Image](https://image.nuxt.com/), [Nuxt Content](https://content.nuxt.com/), and [Nuxt UI](https://ui.nuxt.com/) are some of the official modules developed by the Nuxt team.

### What is Nuxt Content?

Nuxt Content is a file-based CMS that makes working with content easier for Vue developers. Using this module, it is possible to create fully content-driven websites using just Markdown files. It provides syntax highlighting for code snippets in Markdown, interactive Vue components inside content and different utilities including a MongoDB-like API for querying content.

The Nuxt team also offers Nuxt Studio - a pro version of Nuxt Content - with features like collaborative editing, live previews and a UI for working with media assets.

### Setup

To start a fresh Nuxt Content project, we can do so right in the browser using [nuxt.new](https://nuxt.new/), or locally by running the following command:

```bash
npx nuxi@latest init -t content my-minimal-blog
```

To integrate the module to an existing project, we need to first install it and add it to the `modules` property in our `nuxt.config.js`:

```bash
npm install @nuxt/content
```

```js
export default defineNuxtConfig({
  modules: ["@nuxt/content"]
});
```

### Basics

We can configure multiple sources for content in `nuxt.config.js`. By default, all content files are stored in the `content/` folder, and can be in the form of Markdown, YAML, JSON or CSV.

To get started, let's create some content, and ensure we have a catch-all route set up. 

A [catch-all route](https://nuxt.com/docs/guide/directory-structure/pages/#catch-all-route) should already be created by default if we are setting up a Nuxt Content project from scratch, and here is what it looks like initially:

```vue
<!-- pages/[...slug].vue -->
<template>
  <main>
    <ContentDoc />
  </main>
</template>
```

`<ContentDoc>` is a built-in component that takes care of all the fetching and rendering functionality for a single piece of content such as a blog post.

Next, let's create some Markdown files with some content:

**`content/Nuxt.md`**
```md
---
title: Nuxt
description: What is Nuxt?
---

# What is Nuxt?

Nuxt is an open source framework that makes web development intuitive and powerful.

[Learn More](https://nuxt.com)
```

**`content/Nuxt Content.md`**
```md
---
title: Nuxt Content
description: What is Nuxt Content?
---

We can also access our front-matter data in our Markdown.

# {{ $doc.description }}

Nuxt Content makes working with content easy for Vue Developers.

[What is Nuxt?](/nuxt)
```

Nuxt Content will then automatically process our content folder, and generate file-based routes for each content. The file located at `content/Nuxt.md` will be available at `/nuxt`, `content/Nuxt Content.md` at `/nuxt-content`, and so on.

That's it. We now have a minimal yet fully-functioning blog built with Nuxt Content.

## Remote Content

This section will go over how to configure Nuxt Content to work with remote content, specifically with Markdown files from a GitHub repo.

Nuxt Content provides some useful configuration options for fetching, parsing and rendering content. We can configure our Markdown content to have a table of contents and anchor links for our headings. We can add plugins for customizing parsing behavior. We can customize syntax highlighting for our code snippets. We can even set different sources for our content. 

Content-related configurations can be set using the `content` property in `nuxt.config.js` file. 

```js
// nuxt.config.js
export default defineNuxtConfig({
    content: {
        // Custom Configurations
    }
});
```

By default, Nuxt Content is configured to look for local files inside the `content/` directory. But, using the `sources` option, we can tell the module to look for files in different places, which can either be other local files or files hosted on a remote server. Although it's not recommended, we can also override the default content location for local files.

```js
export default defineNuxtConfig({
    content: {
        sources: {
            blog: {
                driver: 'fs',
                prefix: '/blog',
                base: resolve(__dirname, 'articles')
            },
            github: {
                driver: 'github',
                prefix: '/notes',
                repo: "oneminch/notes",
                branch: "main",
                dir: "Glossary"
            },
        }
    }
});
```

In the above snippet, we have added two new sources for our content: one local source and one remote (GitHub). The type of source added is indicated by the `driver` option in our source object:
- The `fs` driver stands for filesystem and indicates our content source is local to the project.
- The `github` driver allows us to map files from a remote GitHub repo to our local project.

**Side Note**: Nuxt Content uses [unstorage](https://unstorage.unjs.io/) under the hood to make this possible. Other types of drivers can be configured according to [the unstorage documentation](https://unstorage.unjs.io/drivers).

Let's see what the `github` configuration above does in action.

Nuxt Content will parse all the markdown files located in the GitHub repo [oneminch/notes](https://github.com/oneminch/notes) under the `Glossary` folder (given by the `dir` property), and make all files available under the `/notes` path (indicated by the `prefix` property). 

For instance, in the repo, I have Markdown files titled `Hoisting.md` and `Server-Side Rendering.md` in the `Glossary` folder. According to our configuration, the contents of these files will be available at the paths `/notes/hoisting` and `/notes/server-side-rendering` respectively, just as working with local content.

We can also use our prefix in different parts of our code that require a path for fetching data. 

**Using the `queryContent()` composable**:

```vue
<script setup>
const { data: notes } = await useLazyAsyncData("my-notes", () =>
    queryContent("/notes").find()
);
</script>
```

**Using the `<ContentList>` component:**

```vue
<template>
    <ContentList path="/notes">
        <template #default="{ list }">
            <a v-for="note in list" :key="note._path" :href="note._path">
              {{ note.title }}
            </a>
        </template>
        <template #not-found>
            <p>No notes found.</p>
        </template>
    </ContentList>
</template>
```

One thing to note is that since Nuxt Content is basically making API calls to GitHub every time we are fetching content, our requests might get rate limited by GitHub. So, it's generally recommended to add a GitHub API token to our configuration following [the unstorage configuration options](https://unstorage.unjs.io/drivers/github#usage).

```js
export default defineNuxtConfig({
    content: {
        sources: {
            github: {
                /* ... */
                token: process.env.GH_TOKEN
            }
        }
    }
})
```

That's it. If you would like to learn more, check out the resources below. Thanks for reading.

## Learn More

- [Nuxt Content in 3 minutes (YouTube)](https://www.youtube.com/watch?v=o9e12WbKrd8)

- [Nuxt Content (Documentation)](https://content.nuxt.com/usage/content-directory)

- [sources - Configuration (Nuxt Content)](https://content.nuxt.com/get-started/configuration#sources)

- [unstorage Drivers](https://unstorage.unjs.io/drivers)