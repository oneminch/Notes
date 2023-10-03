---
alias: R
---
## Concepts

- [React, visualized – react.gg](https://react.gg/visualized)
- [Common Beginner Mistakes with React](https://www.joshwcomeau.com/react/common-beginner-mistakes/)

- composition vs inheritance
- component life cycles
    - useEffect comparison
- rendering
    - [The Interactive Guide to Rendering in React](https://ui.dev/why-react-renders)
    - [Why React Re-Renders](https://www.joshwcomeau.com/react/why-react-re-renders/)
    - [Why React Renders - ui.dev](https://ui.dev/c/react/renders)
    - render props
- higher order components
- hooks
    - [Managing Effects - ui.dev](https://ui.dev/c/react/effects)
- Portals
```jsx
import { createPortal } from "react-dom";

...
return (
    <>
        {createPortal(
            <p>Placed in the <code>body</code> element</p>,
            document.body
        )}
    </>
)
```
- routing
    - react-router
- styling
    - emotion
    - css-in-js
    - styled-components
- API
    - GraphQL - Apollo
    - REST
        - SWR, react-query
            - https://tropicolx.hashnode.dev/infinite-scrolling-in-react-a-practical-guide
- Testing
    - Jest
    - React testing library
    - playwright
- Frameworks
    - Next.js
        - Nextra
- Suspense
- state scheduling and batching
- Forms
    - react-hook-form
    - formik
- A11y in React
    - React-Aria
- server components
    - [Understanding React Server Components – Vercel](https://vercel.com/blog/understanding-react-server-components)
- https://reacthandbook.dev/topics
- [React Design Principles](https://principles.design/examples/reactjs-design-principles)
- [Tao of React - Software Design, Architecture & Best Practices](https://alexkondov.com/tao-of-react/)
---
## Introduction

- React is a [[JavaScript|JS]] library for building UIs.
- Components are reusable building blocks for UIs, and they are at the core of React's architecture.
- JSX syntax is used to include HTML tags inside JS code. A build tool like Babel is used to convert JSX into JS.
- React re-executes and re-evaluates component functions on every state change. 
    - That doesn't necessarily mean a re-render. 
    - Since rendering on every state change might be a potentially expensive operation, React uses the [[virtual DOM]] to render elements which are only affected by the change.
    - Whenever a state changes, the virtual DOM gets updated. React then compares the current snapshot of the virtual DOM to a one taken just before the update, determines which element was affected by the change, and makes updates only to that element on the real DOM.

> [!note]
> We can prevent unnecessary re-evaluations of *functional components* using `React.memo()`. It does this by keeping track of current & previous props for each component, and performing strict equality checks on them whenever state changes. For that reason, state values that are only primitive types are likely to pass this check. 
> 
> `React.memo()` method comes with its own performance costs.

```jsx
{/* How to use memo() */}
const Button = (props) => {
    return <button>{ props.children }</button>
};

export default React.memo(Button);

{/* OR */}
const Button = React.memo((props) => {
    return <button>{ props.children }</button>
});

export default Button;
```

- In React, components are just functions that are written in *PascalCase* and return markup or a markup template. 
    - Only one root element can be returned from a component, just as in Vue. 
    - Conventionally, they are written in and exported as default from a single file with the same name as the component.
- Inside markup, curly braces (`{ }`) can be used to escape into JavaScript syntax.
    - Similar to double curly braces (`{{ }}`) in [[Vue.js]].

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

## Styling

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
    ...
    return (
        <button className={
            `${styles.btn} ${isClicked && styles["btn-clicked"] }`}>
            Submit
        </button>
    );
}
```

- The `Emotion` & `styled-components` libraries are common tools used to create scoped styles for React components.
### Inline Styles

- Inline styles can be applied to a component using the `style` attribute/prop and a set of [[CSS]] properties as a [[JavaScript]] object.

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
### Styled Components


## Components

- In React (JSX), just like in [[Vue.js|Vue]], it's not possible to return more than one root element. Everything needs to be wrapped in a single root element.
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

- React provides an official wrapper ability for such cases called a *Fragment* 
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
    return (<>
        { props.todos.length > 0 ? (<TodoList />) : (<p>No Items Found.</p>) }
    </>)
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
## State Management
### Props

- Props are passed into a component as function arguments defined inside one object, and accessed inside the component as object properties.
- They can also be passed as destructured objects.

> Props / attributes like `className` and `onClick` are reserved on native DOM elements and provide an abstraction of browser provided attributes like `class` and `onclick` respectively.

```jsx
// InfoCard.jsx
export default function InfoCard(props) {  // OR InfoCard({ name, age })
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

> This feature is comparable to how `<slot />`s work in [[Vue.js]].

### Context API

- The Context API allows us to define data in a component and have it be accessed or mutated from any component down the component tree.
    - State is created using `createContext()`.
    - Parent component wraps its child with `<Ctx.Provider>` with a `value` prop set to the state want to pass.
    - State is accessed from the child either using:
        - `<Ctx.Consumer>` (Legacy), or
        - `useContext()` hook.

```js
// ~/store/Ctx.js
import { createContext } from "react";

const MyCtx = createContext();

export default MyCtx;
```

```jsx
{/* ~/components/Parent.jsx */}
import MyCtx from "~/store/Ctx.js";

...
const [someState, setSomeState] = useState("Info")

return (
    <MyCtx.Provider value={someState}>
        <Child />
    </MyCtx.Provider>
)
...
```

- There are a couple of ways to get access to the state from a child component.

```jsx
{/* ~/components/Child.jsx */}
{/* ========== 1 (Legacy) ========== */}
import MyCtx from "~/store/Ctx.js";

...
return (
    <MyCtx.Consumer>
        {(ctx) => {
            return <Header val={ctx} />
        }}
    </MyCtx.Consumer>
);

{/* ========== 2 ========== */}
import { useContext } from "react";

const ctx = useContext(MyCtx);

return <Header val={ctx} />
```

> [!note]
> The Context API is not optimal for high frequency changes.
> 
> As application grows in complexity, using the Context API can get messy and complex.
### Redux

- Redux makes use of subscriptions, triggers and reducer functions.

```js
// ~/src/store/index.js
import { createStore } from "redux"

const initState = { counter: 0, visible: true }

const ctrReducer = (state=initState, action) => {
    if (action.type === "increment") {
        return {
            counter: state.counter + 1,
            visible: state.visible
        }
    }
    if (action.type === "decrement") {
        return {
            counter: state.counter - 1,
            visible: state.visible
        }
    }
    if (action.type === "incrementby") {
        return {
            counter: state.counter + action.amount,
            visible: state.visible
        }
    }
    if (action.type === "togglevisibility") {
        return {
            visible: !state.visible,
            counter: state.counter
        }
    }

    return state;   
}

const store = createStore(ctrReducer)

const ctrSubscriber = () => {
    const latestState = store.getState()
}

store.subscribe(ctrSubscriber)

export default store
```

- In a React application, `redux` is used with `react-redux`. 
    - Root application component needs to be wrapped with the `<Provider>` component from `react-redux` and passed a prop of `store` with the value of our store.
    - `useSelector` and `useDispatch` hooks can be used to get latest values and dispatch actions respectively.

```jsx
{/* ~/src/index.jsx */}
import { Provider } from "react-redux";
import store from "./store/index";
import App from "./App";

const root = ReactDOM.createRoot(document.getElementById("root"));

root.render(
    <Provider store={store}>
        <App />
    </Provider>
);
```

```jsx
import { useSelector, useDispatch } from "react-redux";

const Counter = () => {
    const dispatch = useDispatch();
    const ctr = useSelector((state) => state.counter);    
    const ctrVisible = useSelector((state) => state.visible);    
    
    const decrementHandler = () => {
        dispatch({ type: "decrement" });
    };
        
    const incrementHandler = () => {
        dispatch({ type: "increment" });
    };

    const incrementByHandler = () => {
        dispatch({ type: "incrementby", amount: 5 });
    };

    const toggleCtrHandler = () => {
        dispatch({ type: "togglevisibility" });
    };

    return (
        <>
            {ctrVisible && <div>{ctr}</div>}
            <button onClick={incrementHandler}>+</button>
            <button onClick={incrementByHandler}>+5</button>
            <button onClick={decrementHandler}>-</button>
            <button onClick={toggleCtrHandler}>Toggle Counter</button>
        </>
    )
};
```

> [!important]
> In Redux, it's important that we never mutate the original state object; instead, we return a new state object with updated properties. 
> 
> Old state is *not merged* when an action is dispatched. It must be overwritten. So, it's important that all non-changing state is returned along with changing state. e.g. `{ visible: !state.visible, counter: state.counter }` in the above example.
#### Redux Toolkit

- The above way of using Redux leads to complex code. Redux Toolkit provides a simpler way of managing state with Redux.
- Our store can be simplified as below:
```js
// ~/src/store/index.js
import { createSlice, configureStore } from "@reduxjs/toolkit"

const initCtrState = { counter: 0, visible: true }

const ctrSlice = createSlice({
    name: "counter",
    initialState: initCtrState,
    reducers: {
        increment(state) {
            state.counter++
        },
        decrement(state) {
            state.counter--
        },
        incrementby(state, action) {
            state.counter += action.payload
        },
        togglevisibility(state) {
            state.visible = !state.visible
        },
    }
})

const authSlice = createSlice({
    name: "auth",
    initialState: { isAuth: false },
    reducers: {
        login(state) { state.isAuth = true },
        logout(state) { state.isAuth = false }
    }
})

const store = configureStore({
    // for a single slice
    // reducer: ctrSlice.reducer 
    /* =========================== */
    // multiple slices
    reducer: { ctr: ctrSlice.reducer, auth: authSlice.reducer }
})

export const ctrActions = ctrSlice.actions
export const authActions = authSlice.actions

export default store
```

```jsx
// ~/src/components/Counter.jsx
import { useSelector, useDispatch } from "react-redux";
import { ctrActions } from "~/src/store/index.js";

const Counter = () => {
    const dispatch = useDispatch();
    const ctr = useSelector((state) => state.ctr.counter);
    const ctrVisible = useSelector((state) => state.ctr.visible);
    
    const isAuth = useSelector((state) => state.auth.isAuth);

    const decrementHandler = () => {
        dispatch(ctrActions.decrement());
    };
        
    const incrementHandler = () => {
        dispatch(ctrActions.increment());
    };

    const incrementByHandler = () => {
        dispatch(ctrActions.incrementBy(10));
    };

    const toggleCtrHandler = () => {
        dispatch(ctrActions.toggleCtr());
    };

    return (
        <>
            {ctrVisible && <div>{ctr}</div>}
            <button onClick={incrementHandler}>+</button>
            <button onClick={incrementByHandler}>+5</button>
            <button onClick={decrementHandler}>-</button>
            <button onClick={toggleCtrHandler}>Toggle Counter</button>
        </>
    )
};
```
## Events

- Events in React are similar to props.
    - DOM events on native elements such as `click` and `submit` have a React attribute that emit the same event (`onClick` and `onSubmit`). 
    - These event props take a reference to a pre-defined function as their value. 
    - Triggering such an event calls the referenced function with the event object passed by default.

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

- Hooks can only be called inside component functions or custom hooks at the top level.
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

- Used for referencing a value that's not needed for rendering or for info displayed on the screen.
- Can be used to bind a reference to DOM nodes.
    - Commonly used to bind form elements.
- `useRef` has similar functionality to a class instance variable but for function components.

> [!important]
> Changing a ref doesn't trigger a re-render, and stored information in a ref doesn't reset on every render.
>
> Don't *write* or *read* `ref.current` during rendering. This should instead be done from event handlers or `useEffect`.
> 
> Adding a ref to a `useEffect` dependency array doesn't have any effect.

- Using `ref` on a custom component results in an error. 
- A component doesn't have access to the DOM nodes of other components by default.
- `forwardRef`s can be used by components that want to expose their DOM nodes.

```jsx
{/* Form.jsx */}
export default function MyForm() {
    const inputRef = useRef(null);

    function handleClick() {
        inputRef.current.focus();
    }

    return (<>
        <Input ref={inputRef} />
        <button onClick={handleClick}>Focus</button>
    </>);
}

{/* Input.jsx */}
const Input = forwardRef((props, ref) => {
    return <input {...props} ref={ref} />;
});
```
### `useMemo`

- Allows caching the result of a calculation between re-renders.
- The function passed into `useMemo()` should be a pure function with no arguments, and should return a value.

```jsx
const cachedValue = useCallback(fn, dependencies)
```

```jsx
const sortedItems = useMemo(() => {
    return props.items.sort((a, b) => a - b)
}, [props.items])
```
### `useEffect`

- Track side-effects of state change.
- Useful when we want to execute code as part of a component's render cycle, but not necessarily always when it's re-rendered.
    - e.g. Fetching data on first load.

```jsx
{/* Inside Component */}
useEffect(() => {
    /* Code Block */
}, [])
```

- The first argument of `useEffect()` (setup function) may optionally return a =="clean up"== function. 
    - Every re-render with changed dependencies is preceded by the cleanup function running (if provided) using the old values. 
    - The rest of the logic inside the setup function runs after the "clean up" with the new values.
- The second argument, `[]`, means the code is executed only once on render. To re-execute on each render, the array needs to include the state we need to track. If any of the provided states change, the code inside the function is executed.

> [!note]
> State-updating functions derived from `useState()` are guaranteed to not change on re-render. Thus, it's not necessary to add them to the dependency array.
### `useCallback`

- Cache function definitions between re-renders. It basically does what `React.memo()` or `useMemo()` does, but for functions.
- Unless the dependencies specified change, the function definition doesn't between re-renders.

```jsx
const cachedFn = useCallback(fn, dependencies)
```

> [!note]
> The more specific the state we pass into `useEffect` & `useCallback`, the better the performance. e.g. If we have an object state, passing a specific property instead of the whole object would be more optimal.
> 
> Every state that is referenced inside a `useCallback` & `useEffect` callback should be added as a dependency.

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
        type: "CLICK",
        payload: "Clicked!"
    });
}

const handleSubmit = (formData) => {
    dispatch({
        type: "SUBMIT",
        formData: formData
    });
}
```

```jsx
function reducerFunction(prevState, action) {
    switch (action.type) {
        case "CLICK": {
            console.log(action.payload)
            return action.payload
        }
        case "SUBMIT": {
            console.log(action.formData)
            return action.formData
        }
    }
}
```

### Custom Hooks

- Like any hook, they must start with `use`.
- As a convention, each custom hook can be defined in a [[JavaScript|JS]] file inside a `hooks/` directory.

> [!example] Example: Building a timer using a custom hook

```js
// ~/src/hooks/use-ctr.js
import { useEffect, useState } from "react"

const useCounter = () => {
    const [ctr, setCtr] = useState(0)

    useEffect(() => {
        const interval = setInterval(() => {
            setCtr((prevCtr) => prevCtr + 1)
        }, 1000)

        return () => clearInterval(interval)
    }, [])

    return ctr
}

export default useCounter
```

```jsx
{/* ~/src/components/Counter.jsx */}
import useCounter from "~/src/hooks/use-ctr.js"
...

const ctr = useCounter()

return <p>{ ctr }</p>
```
## Routing

## Project Structure

- A conventional project structure for a vanilla React app might look like this:

```text
.
└── /src
    ├── /assets
    ├── /components
    ├── /services
    ├── /store
    ├── /middleware
    ├── /utils
    ├── /views (or pages)
    ├── index.js
    └── App.js
```

- **assets**: global static assets such as images, svgs, company logo, etc.
- **components**: global shared components (such as layout (wrappers, navigation), form controls, etc.) each organized in their own folder

```text
/components
├── Component.js - The React component
├── Component.styles.js - Styled Components file for the component
└── Component.test.js - The component test file
```

- **services**: JS modules (e.g. a localStorage module)
- **store**: global store
- **utils**: utilities, helpers, and constants (such as validation and conversion functions)
- **views** or **pages**

## Legacy

- In former versions of React, it was necessary to import the library in each JSX file.
### Class-based Components

- A way of creating components before React Hooks were introduced.

```jsx
class Todos extends React.Component {
    constructor () {
        super();
        this.state = {
            todos: [
                {
                    id: 1,
                    title: "Learn React",
                    completed: true
                }
            ]    
        };
    }

    {/* ... */}

    render() {
        return (
            <ul className={classes.todos}>
                {this.state.todos.map(todo => {
                    return <TodoItem todo={todo} key={todo.id} />
                })}
            </ul>
        );
    }
}
```

> [!important]
> - State in class-based components is a property set in the constructor using `this.state`. The component inherits the `setState` method from React that allows changing state. 
> - When setting an object state, React only modifies the key-value pair passed, while keeping other properties unchanged. 
> 
> ```js
> this.setState({ isValid: false })
> // OR
> this.setState((prevState) => {
>     return { isValid: !prevState.isValid }
> })
> ```
> 
> - It's also important to note that event handlers need to bind `this` to work.
> 
> ```jsx
> <button onClick={this.handleClick.bind(this)}>Submit</button>
> ```

#### Side Effects

- To track side effects, class-based components make use of lifecycle methods.
- The ==`componentDidUpdate()`== lifecycle method is called on every re-render. Logic inside this function can be used to check if previous state/props have changed.

```js
componentDidUpdate(prevProps, prevState) {
    if (prevState.val !== this.state.val) {
        // Logic
    }
}
```

- In functional components, this is equivalent to:

```js
useEffect(() => {
    // Logic
}, [val])
```

- The ==`componentDidMount()`== method is executed on initial render. In functional components, it is equivalent to using `useEffect()` without passing any dependencies.

```js
useEffect(() => {
    // Logic
}, [])
```

- The ==`componentWillUnmount()`== method is called right before a component is removed from the DOM. In functional components, it is equivalent to returning a cleanup function in `useEffect()`.

```js
useEffect(() => {
    return () => { /* Logic */ }
}, [])
```

#### Error Boundaries

- React components that allow JavaScript error handling in their child component tree. 
- They catch errors during rendering, in lifecycle methods, and in constructors of all child components.

```jsx
{/* ErrorBoundary.jsx */}
class ErrorBoundary extends React.Component {
    constructor () {
        super();
        this.state = {
            caughtError: false    
        };
    }

    componentDidCatch(error) {
        this.setState({ caughtError: true });
    }

    render() {
        if (this.state.caughtError) {
            return <p>An Error Has Occured!</p>;
        }
        return this.props.children;
    }
}

{/* SomeComponent.jsx */}
<ErrorBoundary>
    <SomeChildComponent />
</ErrorBoundary>
```

- Any errors thrown from `<SomeChildComponent />` are caught and handled by the `<ErrorBoundary>` component.
## React Best Practices

- Never define a component inside another component.
    - Every component should be defined at the top level in a file.

---
## Further

### Books 📚

- Learning React (Alex Banks)
### Ecosystem 🏵

#### Assorted

- Mantine
- TanStack
- useHooks
#### Meta-frameworks

- Next.js
    - Nextra
- Remix
#### State Manangement

- Redux
- Zustand
#### UI

- Radix UI
    - Shadcn-UI
- Tailwind CSS
- Material UI
- Chakra UI
- Mantine
- NextUI
### Learn 🧠

- [React: The Complete Course - Udemy](https://www.udemy.com/course/react-the-complete-guide-incl-redux/)

- [Learn React](https://react.dev/learn)

- [React 2025 (by Lee Robinson)](https://react2025.com/)

- [React Handbook](https://reacthandbook.dev/)

### Reads 📄

- [Why React?](https://ui.dev/c/react/why-react)

- [React Architecture: How to Structure and Organize a React Application - Tania Rascia](https://www.taniarascia.com/react-architecture-directory-structure/)

- [Rendering Patterns](https://www.patterns.dev/posts/rendering-patterns)
### Resources 🧩

- [enaqx/awesome-react](https://github.com/enaqx/awesome-react#readme)

### Roadmaps 🗺

- [React Roadmap](https://roadmap.sh/react)