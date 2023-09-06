---
alias: Vue
---
## Examples

**Single HTML File**

```html
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>

<div id="app">{{ message }}</div>

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

**HTML + JS**

```html
<!-- index.html -->
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>

<div id="app"></div>

<script type="module">
    import MyComponent from "./my-component.js";
    const { createApp } = Vue;
    
    createApp(MyComponent).mount("#app");
</script>
```

```js
// my-component.js
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


---
## Further
### Ecosystem 🏵

#### Meta-frameworks 

- Nuxt 
- VitePress
- VuePress
#### Routing

- Vue Router
#### State Management

- Pinia
### Learn 🧠

- [Vue: The Complete Guide - Udemy](https://www.udemy.com/course/vuejs-2-the-complete-guide/)

### Resources 🧩

- [vuejs/awesome-vue](https://github.com/vuejs/awesome-vue#readme)

### Roadmap 🗺

- [Vue.js Roadmap](https://roadmap.sh/vue)