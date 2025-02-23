---
aliases:
  - Vue.js
---

> [!example]- Learning Roadmap
> > [Vue Developer Roadmap](https://roadmap.sh/vue)
> - Official Guide
>     - https://vuejs.org/guide/introduction.html
> - API Styles
>     - Options
>     - Composition
> - Reactivity
>     - https://www.youtube.com/watch?v=NZfNS4sJ8CI
> - State Management
>     - https://icarusgk.hashnode.dev/state-management-in-vue-3
> - Design Patterns
>     - https://www.patterns.dev/vue
>     - https://michaelnthiessen.com/12-design-patterns-vue
> - Suspense
>     - https://www.youtube.com/watch?v=GQpKm_CNH4A
> - Testing
>     - https://vuejs.org/guide/scaling-up/testing
>     - https://test-utils.vuejs.org/guide/essentials/a-crash-course.html

---
## Setup

**Scaffolding a Starter Vue App**

```bash
npm create vue@latest
# OR
pnpm create vue@latest
```

**Single HTML File**

```html
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>

<div id="app"></div>

<script type="module">
    const { createApp } = Vue

    createApp({
        data() {
            return { count: 0 };
        },
        methods: {
            increment() {
                this.count += 1;
            },
        },
        template: `
            <div>
                <button v-on:click="increment">+</button>
                <p>Count: {{ count }}</p>
            </div>
        `
    }).mount('#app')
</script>
```

**HTML + JS / SFC (`.vue`)**

```html
<!-- index.html -->
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>

<div id="app"></div>

<script type="module">
    import MyCounter from "./my-counter.js"; // or ./my-counter-sfc.vue
    const { createApp } = Vue;
    
    createApp(MyCounter).mount("#app");
</script>
```

```js
// my-counter.js
export default {
    data() {
        return { count: 0 };
    },
    methods: {
        increment() {
            this.count += 1;
        },
    },
    template: `
        <div>
            <button v-on:click="increment">+</button>
            <p>Count: {{ count }}</p>
        </div>
    `
};
```

## Styling

### `class`

```vue
<script setup>
const item = ref({
    label: "Hello, Vue!",
    isHeading: true,
    isImportant: true
});
</script>

<template>
    <p 
        class="static-class"
        :class="{
            'font-bold': item.isImportant,
            'text-xl': item.isHeading
        }">
        {{ item.label }}
    </p>
    <!-- OR -->
    <p
        :class="[
            'static-class',
            { 'font-bold': item.isImportant },
            { 'text-xl': item.isHeading }
        ]">
        {{ item.label }}
    </p>
    <!-- OR -->
    <p
        :class="[
            'static-class',
            headingClass,
            item.isImportant ? imptClass : '',
            // OR
            { [imptClass]: item.isImportant }
        ]">
        {{ item.label }}
    </p>
</template>
```

- Values passed to `class` on a component with a single root element are added to the component's root element and merged with any existing classes.
- For components with multiple root elements, the `$attrs` component property can be used to define which element will receive this class.

```vue
<!-- <Text> SFC using $attrs (fallthrough attributes): -->
<p :class="$attrs.class">Hi!</p>
<span>This is a child component</span>

<!-- Pass class to component: -->
<Text class="baz" />

<!-- Renders: -->
<p class="baz">Hi!</p>
<span>This is a child component</span>
```

### `style`

```vue
<script setup>
const styleObject = reactive({
    color: 'red',
    fontSize: '30px',
    'font-family': 'Inter'
});
</script>

<template>
    <div :style="styleObject"></div>
</template>
```

- An array of multiple style objects can also be used. Vue will merge the objects and apply them to the same element.

```vue
<h1 :style="[baseStyles, overridingStyles]"></h1>
```

> [!note] Auto-prefixing
> Vue automatically adds vendor prefixes for CSS properties that require it. It checks for browser support at runtime to achieve this.

## Conditional Rendering

- When using `v-if`/`v-else-if`/`v-else` on a `<template>` element, it serves as an invisible wrapper. The `<template>` element will not be included in the final rendered result.

```vue
<template v-if="isVisible">
  <h1>Heading</h1>
  <p>Lorem Ipsum ...</p>
</template>
```

### `v-if` vs. `v-show`

- `v-if` ensures that event listeners and child components are properly destroyed and re-created based on the condition provided. 
    - The conditional block is only rendered when the condition is true for the first time.
    - It has higher toggle costs.
    - Prefer `v-if` for conditions that are unlikely to change at runtime.
- With `v-show`, an element will always be rendered and remain in the [[DOM]]. 
    - Using the directive only toggles the CSS `display` property.
    - It doesn't support the `<template>` element.
    - It has higher initial render costs.
    - Prefer `v-show` for frequent toggles.

## List Rendering

```vue
<div v-for="item in items" :key="item"></div>

<!-- Alias for 'in' -->
<div v-for="item of items" :key="item"></div>

<!-- Iterate on a range (from 1 to 5) -->
<span v-for="n in 5" :key="n">{{ n }}</span>

<!-- With a Component -->
<BlogPost v-for="item in items" :key="item.id" />
```

- `v-for` can be used to iterate through properties of an object.

```vue
<script setup>
const myObject = reactive({
    foo: 'bar',
    baz: 'boo'
})
</script>

<template>
    <ul>
        <li v-for="(value, key, index) in myObject" :key="key">
          {{ index }}. {{ key }}: {{ value }}
        </li>
    </ul>
</template>
```

- Similar to `v-if`, `<template>` can be used with `v-for` to render a block of multiple elements.

> [!important]
> When `v-if` and `v-for` exist on the same node, `v-if` will have a higher priority. That means `v-if` will not have access to variables from `v-for`'s scope. The solution is to wrap the `v-if` node in a `<template>` and using `v-for` on the template.

```vue
<template v-for="post in posts" :key="post.id">
    <li v-if="post.published">
        {{ post.title }}
    </li>
</template>
```

> [!note] Why Not to Use Array Index as Key?
> - If the list order changes (e.g., sorting), the index-based keys will no longer correspond to the same data items, which causes Vue to unnecessarily re-render elements.
> - Adding or removing items from the list can cause unexpected behavior in component state and DOM updates.
> - It's always recommended to use a unique identifier from data as the key, such as an ID from a database or any unique property of the item.

## Composables

- In the context of Vue apps, a composable is a function that leverages the Composition API to encapsulate and reuse stateful logic.
- Similar to hooks in [[React]], composables can be used to manage state that changes over time or reactive state.
- A function is not considered a composable, if 
    - it does not manage any reactive state 
    - it doesn't register any lifecycle hooks
    - it doesn't provide/inject anything.

```ts
import { ref, onMounted, onUnmounted } from 'vue';

export const useMousePosition = () => {
    const x = ref(0);
    const y = ref(0);
    
    const updatePosition = (e: MouseEvent) => {
        x.value = e.pageX;
        y.value = e.pageY;
    }
    
    onMounted(() => window.addEventListener('mousemove', updatePosition));
    onUnmounted(() => window.removeEventListener('mousemove', updatePosition));
    
    return { x, y };
}
```

## Performance

- [The Ultimate Guide to Vue Performance, a Vue.js video course](https://vueschool.io/courses/the-ultimate-guide-to-vue-performance)

## Advanced

### Rendering Mechanism

- **Compile** 
    - Vue templates get compiled into render functions (functions that return [[Virtual DOM]] trees)
    - Can be done ahead-of-time (build step) or on-the-fly (runtime compiler).
- **Mount**
    - The runtime renderer calls the render functions, walks the returned VDOM tree, and constructs a real DOM tree from it.
- **Patch** / **Diffing** / **Reconciliation**
    - When a dependency used during mount changes, the effect re-runs, creating a new, updated [[Virtual DOM|VDOM]] tree. 
    - The runtime renderer walks the new tree, compares it with the old one, and applies necessary updates to the actual [[DOM]].

> [!quote] Render Pipeline
> ![[vue.rendering-mechanism.png]]
> 
> **Source**: [Vue.js](https://vuejs.org/guide/extras/rendering-mechanism.html)

---
## Further

## Books 📚

- Fullstack Vue (Hassan Djirdeh)

### Code 👨🏽‍💻

- [vuejs / vitepress (GitHub)](https://github.com/vuejs/vitepress)

### Ecosystem 🌳

#### Forms

- FormKit

#### Meta-frameworks 

- Nuxt 
- VitePress
- VuePress

#### Routing

- Vue Router

#### State Management

- Pinia

#### UI

- Radix Vue
- Storefront UI

### Learn 🧠

- The Framework Field Guide (Corbin Crutchley)

- [Vue: The Complete Guide (Udemy)](https://www.udemy.com/course/vuejs-2-the-complete-guide/)

- [Common Vue.js Mistakes and How to Avoid Them (VueSchool.io)](https://vueschool.io/courses/common-vue-js-mistakes-and-how-to-avoid-them)

### Resources 🧩

- [vuejs/awesome-vue](https://github.com/vuejs/awesome-vue#readme)

### Roadmap 🗺

- [Vue.js Roadmap](https://roadmap.sh/vue)