# ==???==

- What is a conventional react project architecture / structure?
- Functional vs class components
- composition vs inheritance
- component life cycles
- hooks
    - builtin hooks
        - useref
        - useeffect
            - cleanup functions
    - custom hooks
- Portals
- routing - react router
- state management
    - context
    - Redux
- styling
    - emotion
    - tailwind
- API
    - GraphQL - Apollo
    - REST
        - SWR, react-query
- Testing
    - Jest
    - React testing library
    - playwright
- Frameworks - Next.js, remix
- Forms

# ==???==


- React is a [[JavaScript|JS]] library for building UIs.
- Components are reusable building blocks for UIs, and they are at the core of React's architecture.
- JSX syntax is used to include HTML tags inside JS code. A build tool like Babel is used to convert JSX into JS.

> [!note]
> In React, components are just functions that are written in *PascalCase* and return markup or a markup template. Only one root element can be returned from a component just as in Vue. 
> 
> Conventionally, they are written in and exported as default from a single file with the same name as the component.

- Inside markup, curly braces (`{ }`) can be used to escape into JavaScript syntax.
    - Similar to double curly braces (`{{ }}`) in [[VueJS]].

```jsx
function Component() {
    return (
        <p>Current Year: { new Date().getFullYear() }</p>
    )
}
```

## Setup

- `index.html` - Main entry HTML file
    - Typically contains a root element, `<div>` with an `id` attribute which is where React renders the root component.
    - Contains a `<script>` tag with `type='module'` and `src` that links to the main entry JS file
- `main.js` or `main.jsx` - Main entry JS file
    - Inserts the root React component into the root element in `index.html`.

```jsx
import React from "react";
import ReactDOM from "react-dom/client"
import App from "./App.jsx"  // Root component

const rootEl = ReactDOM.createRoot(document.querySelector("#root"));
rootEl.render(<App />)
```

- `App.js` or `App.jsx` - Root component
    - The root component of the application rendered inside the root element in `index.html`
    - Just like any React component.

```jsx
function App() {
    // Some component logic

    return (
        <h1>Hello, React!</h1>
    )
}
```

## Styles

- By convention, CSS files with styles specifically for a component have the same name as the component file. They can be imported in the component file like a JS module.

```jsx
// App.jsx
import "./App.css"
```

> [!important]
> By default, styles defined in separate CSS files are not scoped to a component.

### CSS Modules

- CSS Modules are a common way of scoping styles to a component. 
- Tools like `create-react-app` and `vite` support CSS modules. They basically attach a unique identifier to each component and list the styles with the unique ID as a selector.

```css
/* Button.module.css */
.btn {
    background: "red";
}

.btn-clicked {
    background: "crimson";
}
```

```jsx
import styles from "./Button.module.css";

const Button = () => {
    return (
        <button className={
            `${styles.btn} ${isClicked && styles["btn-clicked"] }`}>
            Submit
        </button>
}
```

- The `Emotion` & `styled-components` libraries are common tools used to create scoped styles for React components.

### Inline Styles

- Inline styles can be applied to a component using the `style` attribute/prop and an object of [[CSS]] properties in [[JavaScript]] notation.

```jsx
<section style={{ height: '50%', borderColor: 'lightcoral' }}>
    { props.children }
</section>
```

- Since the syntax is all [[JavaScript]], we can apply styles conditionally.

```jsx
<button style={{ background: isClicked ? "gray" : "goldenrod" }}>
    Submit
</button>
```

## Components

- In React (JSX), just like in [[Vue]], it's not possible to return more than one root element. Everything needs to be wrapped in a single root element.
- One way to work around this is to return an array of JSX elements. But, just like rendering lists, each component will require its own unique key.

```jsx
const App = () => {
    return [
        <SubmitButton key="submitButton" />,
        <CancelButton key="cancelButton" />
    ]
}
```

- Another way to work around this pattern is to use a helper function that serves as a wrapper component.

```jsx
{/* ~/helpers/wrapper.js */}
export default function Wrapper(props) {
    return props.children;
}
```

```jsx
{/* App.jsx */}
import wrapper from "~/helpers/wrapper";

const App = () => {
    return (
        <Wrapper>
            <SubmitButton />,
            <CancelButton />
        </Wrapper>
    )
}
```

- React provides an official wrapper ability for such cases called a fragment 
    - `<React.Fragment></React.Fragment>` or `<></>` (empty tags)

```jsx
import React from "react";

const App = () => {
    return (
        <React.Fragment>
            <SubmitButton />,
            <CancelButton />
        </React.Fragment>
    )
}
```

### Props

- Props are passed into a component as function arguments defined inside one object, and accessed inside the component as object properties.
- They can also be passed as destructured objects.

> Props / attributes like `className` and `onClick` are reserved on native DOM elements and provide an abstraction of browser provided attributes like `class` and `onclick` respectively.

```jsx
// InfoCard.jsx
export default function InfoCard(props) {  // same as function InfoCard({ name, age })
    return (
        <div>
            <p>Name: { props.name }</p>
            <p>Age: { props.age }</p>
        </div>
    )
}

// App.jsx
export default function App() {
    return (
        ...
        <InfoCard name="Jane Doe" age="30" />
        ...
    )
}
```

> [!note]
> Custom components don't support attributes like `className` by default. To attach a pre-defined attribute (e.g. `className`) to a custom component, we need to treat it like a regular custom prop and use the prop value in the native DOM element used to define the component.

```jsx
{/* App.jsx */}
const App = (props) => {
    return (
        <FancyButton className="px-4 py-2">Submit<FancyButton/>
    );
}

{/* FancyButton.jsx */}
const FancyButton = (props) => {
    return (
        <button className={props.className}>{ props.children }</button>
    );
}
```

**How to render data between opening and closing tags of a component?**

```jsx
{/* App.jsx */}
const App = (props) => {
    return (
        <FancyButton>Submit<FancyButton/>
    )
}

{/* FancyButton.jsx */}
const FancyButton = (props) => {
    return (
        <button className="fancy-btn">{ props.children }</button>
    )
}
```

> This feature is comparable to how `<slot />`s work in [[VueJS]].

## Rendering

### List Rendering

- If React encounters a [[JavaScript|JS]] array of components in JSX, it renders them side by side in the [[DOM]].

```jsx
const App = (props) => {
    return (
        <section>
            {[<Header />, <Article />, <Footer />]}
        </section>
    )
}
```

- This same logic is used to render a list of components using a loop.

```jsx
const TodoList = (props) => {
    return (
        <ul>
            { props.todos.map((todo) => (<Todo data={todo} key={todo.id} />)) }
        </ul>
    )
}
```

### Conditional Rendering

- Components can be rendering conditionally in serveral ways.

```jsx
{/* (1) */}
const App = (props) => {
    return (
        <>
            { props.todos.length > 0 ? (<TodoList />) : (<p>No Items Found.</p>) }
        </>
    )
}

{/* (2) */}
const App = (props) => {
    return (
        <>
            { props.todos.length > 0 && (<TodoList />) }
            { props.todos.length == 0 && (<p>No Items Found.</p>) }
        </>
    )
}

{/* (3) */}
const App = (props) => {
    let myList = (<p>No Items Found.</p>)

    if (props.todos.length > 0) {
        myList = (<TodoList />)
    }

    return myList
}
```

## Events

- Events in React are similar to props.
    - DOM events on native elements such as `click` and `submit` have a React attribute that emit the same event (`onClick` and `onSubmit`). 
    - These event props take a reference to a pre-defined function as their value. 
    - Triggering such an event calls referenced function with the event object passed by default.

```jsx
{/* MyButton.jsx */}
const MyButton = () => {
    const handleClick = () => console.log("Clicked!");

    return (
        <button onClick={handleClick}>Click</button>
    )
}
```

- To pass arguments to a function, we need to reference an anonymous inline function that evokes the function we want to call with the arguments we want.

```jsx
{/* MyButton.jsx */}
const MyButton = () => {
    const handleClick = (msg) => console.log(msg);

    return (
        <button onClick={(e) => handleClick("Clicked!")}>Click</button>
    )
}
```

### Passing Data to Parent

- Data can be passed from a parent to a child component using props. Custom events can be used to pass data from child to a parent.

```jsx
{/* Parent.jsx */}
const Parent = () => {
    const handleSendData = childData => console.log(childData)

    return (
        <Child onSendData={handleSendData} />
    );
}

{/* Child.jsx */}
const Child = (props) => {
    const localData = { a: 1, b: 2 };

    const sendData = (data) => props.onSendData(data)

    return (
        <button onClick={() => sendData(localData)}>Send</button>
    );
}
```

## Hooks

### `useState`

```jsx
import { useState } from "react"

export default function Counter() {
    const [currCount, setCount] = useState(0);

    return (
        <button onClick={() => setCount(prevCount => prevCount+1)}>
            Count: { currCount }
        </button>
    )
}
```

> [!note]
> `useState` is scoped to each component instance.

### `useRef`

- Bind state to form elements.

### `useEffect`

- Track side-effects of state change.

```jsx
{/* Inside Component */}
useEffect(() => {
    /* Code Block */
}, [])
```

- The second argument, `[]`, means the code is executed only once on render. To re-execute on each render, the array needs to include the state we need to track. If any of the provided states change, the code inside the function is executed.

> [!note]
> The more specific the state we pass into `useEffect`, the better the performance. e.g. If we have an object state, passing a specific property instead of the whole object would be more optimal.

### `useReducer`

- More complex and powerful state management.

```jsx
{/* Inside Component */}
const [state, dispatch] = useReducer(
    reducerFunction,
    initialState,
    initialFunction
);

const handleClick = () => {
    dispatch({
        type: "click",
        payload: "Clicked!"
    });
}

const handleSubmit = (formData) => {
    dispatch({
        type: "submit",
        formData: formData
    });
}
```

```jsx
function reducerFunction(prevState, action) {
    switch (action.type) {
        case "click": {
            return console.log(action.payload)
        }
        case "submit": {
            return console.log(action.formData)
        }
    }
}
```

## Legacy

- In former versions of React, it was necessary to import the library in each JSX file.

## Further

### Learn 🧠

- [React: The Complete Course - Udemy](https://www.udemy.com/course/react-the-complete-guide-incl-redux/)

- [Rendering Patterns](https://www.patterns.dev/posts#rendering-patterns)

### Roadmaps 🗺

- [React Roadmap](https://roadmap.sh/react)