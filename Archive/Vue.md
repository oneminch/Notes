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
</template>
```

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

---
## Further

## Books 📚

- Fullstack Vue (Hassan Djirdeh)

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