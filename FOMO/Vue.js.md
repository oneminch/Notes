---
alias: Vue
---

## Concepts

- Official Guide
    - https://vuejs.org/guide/introduction.html
- Reactivity
    - https://www.youtube.com/watch?v=NZfNS4sJ8CI
- State Management
    - https://icarusgk.hashnode.dev/state-management-in-vue-3
- Design Patterns
    - https://www.patterns.dev/vue

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

## Bookmarks

- [Data Fetching Patterns in Single-Page Applications](https://martinfowler.com/articles/data-fetch-spa.html)

---
## Further

## Books 📚

- Fullstack Vue (Hassan Djirdeh)

### Ecosystem 🏵

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

- [The Framework Field Guide (Unicorn Utterances)](https://unicorn-utterances.com/collections/framework-field-guide)

- [Vue: The Complete Guide (Udemy)](https://www.udemy.com/course/vuejs-2-the-complete-guide/)

- [Vue.js Courses (Vue School)](https://vueschool.io/courses)

### Resources 🧩

- [vuejs/awesome-vue](https://github.com/vuejs/awesome-vue#readme)

### Roadmap 🗺

- [Vue.js Roadmap](https://roadmap.sh/vue)