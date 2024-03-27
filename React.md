---
alias: R
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
> We can prevent unnecessary re-evaluations of *functional components* using `React.memo()`. 
>
> `React.memo()` takes in a React component as an argument and returns a new component that will only re-render if its props change.
> 
> It does this by keeping track of current & previous props for each component, and performing strict equality checks on them whenever state changes. For that reason, state values that are only primitive types are likely to pass this check. 
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

- When React renders a component,
    - It creates a snapshot of the component which contains information about that component: props, state, event handlers.
    - It uses the description for the UI to update the view.

> [!important]
> A re-render occurs only when the state of a component changes.
> 
> A component will NOT re-render because its props change.

- When an event handler is invoked, if that event handler contains an invocation of `useState`'s setter/updater function, our component state changes. React notices that there is a new state that is different from the one in the snapshot, and triggers a re-render, which creates a new snapshot and updates the view.

> [!important]
> React will only re-render **once** per event handler, even if multiple pieces of state have been updated.

- It's important to note that a re-render occurs only after React has taken into account every state-updating function invocation inside an event handler, and it's sure of the final state value. 
- When React comes across multiple invocations of the same state-updating function, it will use the result of the last invocation as the new state.
    - To use the values of the previous invocation in the current invocation, we can pass a callback function to our state-updating function.

```js
{/* For this event handler, React will re-render once per click */}
const handleClick = () => {
    setCounter(count + 1) // 1
    setCounter(count + 1) // 1
    setCounter(count + 1) // 1
}

{/* Passing the previous state */}
const handleClick = () => {
    setCounter(1)          // 1
    setCounter(c => c + 1) // 2
    setCounter(c => c + 3) // 5
}
```

- It's also important to note that whenever state changes, React will re-render the component that owns that state and all of its child components - regardless of whether or not those child components accept any props from their parent.
    - To ensure a child component renders only when its own props change, we can use `React.memo()`. 

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
> `useState` is scoped to each component instance, and state-setter functions are asynchronous.

- `useState` has *lazy initialization*, which is a performance optimization. 
    - If a function is passed to `useState`, React will only call `useState` when it needs the initial value (or when the component initially renders).

```jsx
const [count, setCount] = useState(() => {
    return Number(window.localStorage.getItem('count')) || 0;
})
```

### `useRef`

- Used for referencing a value that's not needed for rendering or for info displayed on the screen.
- It's also used to preserve a value across renders (non-visual state like timer ids or DOM nodes).
- Can be used to bind a reference to DOM nodes.
    - Commonly used to bind form elements.
- `useRef` has similar functionality to a class instance variable but for function components.

> [!important]
> Changing a ref doesn't trigger a re-render, and stored information in a ref doesn't reset on every render.
>
> Don't *write* or *read* `ref.current` during rendering. This should instead be done from event handlers or `useEffect`.
> 
> Adding a ref to a `useEffect` dependency array doesn't have any effect.

#### `forwardRef`

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
const cachedValue = useMemo(fn, dependencies)
```

```jsx
const sortedItems = useMemo(() => {
    return props.items.sort((a, b) => a - b)
}, [props.items])
```

- It is generally considered a good idea to memoize state inside context providers.

```jsx
const AuthCtx = createContext({});

function AuthProvider({ user, status, children }){
    const memoizedValue = useMemo(() => {
        return {
            user,
            status,
        };
    }, [user, status]);

    return (
        <AuthCtx.Provider value={memoizedValue}>
            {children}
        </AuthCtx.Provider>
    );
}
```

### `useEffect`

- Track side-effects of state change.
- It removes side effects from the rendering flow, and delays their execution until after rendering is complete.
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
- The second argument (dependency array), `[]`, means the code is executed only once on render. To re-execute on each render, the array needs to include the state we need to track. If any of the provided states change, the code inside the function is executed.

> [!note]
> State-updating functions derived from `useState()` are guaranteed to not change on re-render. Thus, it's not necessary to add them to the dependency array.

- Using `await` inside the `useEffect` callback can be tricky, even if the callback function is prefixed with the `async` keyword. 
    - `useEffect(async () => {})` doesn't work.
    - To achieve this effect, we need to declare a separate `async` function inside our callback.

```jsx
useEffect(() => {
    async function runEffect() {
        // Effect logic
    }
    
    runEffect();

    return () => {
        // Cleanup logic here
    }
}, [dependency]);
```

### `useLayoutEffect`

- `useLayoutEffect` has a similar functionality as `useEffect`, but it fires before the browser repaints the screen.

### `useCallback`

- Cache function definitions between re-renders. It basically does what `React.memo()` or `useMemo()` does, but for functions.
- Unless the dependencies specified change, the function definition doesn't between re-renders.

```js
const cachedFn = useCallback(fn, dependencies)
```

```jsx
useCallback(function handleClick(){}, []);

// ...Is syntactic sugar for:

useMemo(() => function handleClick(){}, []);
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

## Data Fetching

- Client-side data fetching makes use of `useState` to store our fetch response, and `useEffect` to make the request.
    - Alternatively, we can extract the data fetching function outside the component to make an async request before the component is rendered.

```jsx
{/* Data Fetching using fetch & useEffect */}
function Users() {
    const [usersList, setUsersList] = useState(null)
    const [isLoading, setLoading] = useState(true)
 
    useEffect(() => {
        fetch('/api/users')
            .then((res) => res.json())
            .then((data) => {
                setUsersList(data)
                setLoading(false)
            })
    }, [])

    if (isLoading) return <p>Loading Users...</p>
    if (!usersList) return <p>No Users Found.</p>
    
    return <UsersList data={usersList} />
}
```

- Another approach for data fetching is to create a custom hook:

```js
const useFetch = (url) => {
    const [data, setData] = useState(null);
    const [error, setError] = useState(null);
    const [loading, setLoading] = useState(true);

    useEffect(() => {
        const getData = async () => {
            try {
                const res = await axios.get(url);
                setData(res.data);
            } catch (err) {
                console.error(`Error: ${err}`);
                setError(err);
            } finally {
                setLoading(false);
            }
        };
        getData();
    }, []);

    return {
        data,
        loading,
        error,
    };
};
```

- Popular libraries such as SWR and Tanstack Query provide powerful features fetching data on the client-side. 
    - Caching, revalidation, and interval-based re-fetching are among some of the features of SWR.

```jsx
{/* Data Fetching using SWR */}
import useSWR from 'swr'
 
const fetcher = (...args) => fetch(...args).then((res) => res.json())
 
function Users() {
    const { data, error, isLoading } = useSWR('/api/users', fetcher)
 
    if (error) return <div>Failed to Load Users.</div>
    if (isLoading) return <p>Loading Users...</p>
    
    return <UsersList data={data} />
}
```

- When working with GraphQL APIs, popular clients like Apollo Client and Relay can be used.
## State Management

- ==State scheduling== is the process of determining when to update the state of a component. 
    - React provides methods that allow developers to schedule state updates, which can be processed either synchronously or asynchronously.
    - These can be `setState` in class components and the state updater function in functional components.
- ==Batching== is the process of grouping multiple state updates into a single re-render for better performance. 
    - In React versions 17 and prior, updates inside React event handlers were batched, but updates inside of promises, `setTimeout`, native event handlers, or any other event were not batched by default. 
    - In React 18, a new feature called Automatic Batching was introduced, which enables batching of all the state updates regardless of where they are called.
    - Automatic batching ensures that state updates invoked from any location, such as simple functions containing multiple state updates, web APIs, and interfaces like `setTimeout`, fetch, or promises containing multiple state updates, will be batched by default. 
        - This can significantly improve the performance of React applications, especially for larger applications with many state updates.

```jsx
const Counter = () => {
    const [count, setCount] = useState(0)

    const incrementByOne = () => {
        // These updates are batched.
        setCount(count + 1)
        setCount(count + 1)
        setCount(count + 1)
    }
    
    const incrementByFive = () => {
        setCount(count + 1)
        setCount(count => count + 1)
        setCount(count + 2)
        setCount(count => count + 3)
    }
    
    return (<>
        <p>Count: {count}</p>
        <button onClick={incrementByOne}>Increment by 1</button>
        <button onClick={incrementByFive}>Increment by 5</button>
    </>)
}
```

- In the snippet below, both updates to `count` in `setTimeout` will be batched into a single re-render, and both updates to `name` in `fetch` will be batched into a single re-render.
    - The component will only re-render twice (once for `count` updates and once for `name` updates) rather than four times if the updates were not batched.

```jsx
const Example = () => {
    const [count, setCount] = useState(0);
    const [name, setName] = useState('');

    useEffect(() => {
        setTimeout(() => {
            setCount(count + 1);
            setCount(count + 1);
        }, 1000);
        
        fetch('https://api.example.com/user')
            .then(response => response.json())
            .then(data => {
                setName(data.name);
                setName(data.name + '!');
            });
    }, []);

    return (
        <div>
            <p>Count: {count}</p>
            <p>Name: {name}</p>
        </div>
    );
}
```

### Props

- Props are ==immutable== pieces of data.
- They are passed into a component as function arguments defined inside one object, and accessed inside the component as object properties.
- They can also be passed as destructured objects.

> Props / attributes like `className` and `onClick` are reserved on native DOM elements and provide an abstraction of browser provided attributes like `class` and `onclick` respectively.

```jsx
// PersonCard.jsx
export default function PersonCard(props) {  // OR PersonCard({ name, age })
    return (
        <div>
            <PersonDetails name="Jane Doe" age="30" />
            { /* OR <PersonDetails { ...props } /> */ }
        </div>
    )
}

// App.jsx
export default function App() {
    return (
        ...
        <PersonCard name="Jane Doe" age="30" />
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

## Styling

- By convention, CSS files with styles specifically for a component have the same name as the component file. They can be imported in the component file like a JS module.

```jsx
// App.jsx
import "./App.css" // or "./App.scss"
```

> [!important]
> By default, styles defined in separate CSS files are not scoped to a component.

- `classnames` and `clsx` are popular utilities used for constructing `className` strings conditionally.
### CSS Modules

- CSS Modules are a common way of scoping styles to a component. 
- A CSS Module is a CSS file which declares styles that are scoped by default.
- Tools like `create-react-app` and `vite` support CSS Modules out of the box. 
    - They basically attach a unique identifier to each component and list the styles with the unique ID as a selector.

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

### CSS-in-JS

- The `emotion` & `styled-components` libraries are common CSS-in-JS tools used to create scoped styles for React components.
- `styled-components` provide features such as deferred/lazy CSS injection.

```jsx
import styled from 'styled-components'

const Title = styled.h1`
    font-size: 1.5rem;
    color: grey;
    text-align: center;
`;

const App = () => {
    return (
        <Title>Hello, React!</Title>
    )
}

export default App;
```

- Other libraries such as `emotion`, `styled-jsx` (by Vercel), StyleX, and `vanilla-extract` provide an alternative approach to writing CSS-in-JS.
    - `emotion` even provides a similar syntax as `styled-components` via `@emotion/styled`.

```jsx
import { css } from '@emotion/react'

const color = 'grey'

render(
    <h1
        css={css`
            font-size: 1.5rem;
            color: ${color};
            text-align: center;
        `}>
        Hello, React!
    </h1>
)
```

### Utility-First

- CSS frameworks such as Tailwind CSS and UnoCSS provide a utility-first approach to styling components.

```jsx
<button class="py-2 px-4 rounded bg-indigo-400 focus:ring">Submit</button>
```

### Component Libraries

- Popular UI component libraries for React apps:
    - Radix UI
        - Shadcn-UI
    - Chakra UI
    - NextUI
    - Ant Design
    - Mantine
    - Material UI

## Forms

- One of the ways we can build forms involves accessing the DOM nodes directly using refs.

```jsx
const Form = () => {
    const inputRef = useRef()

    const submit = (e) => {
        e.preventDefault()
        const text = inputRef.current.value
        console.log(text)
        inputRef.current.value = ""
    }

    return (
        <form onSubmit={submit}>
            <input ref={inputRef} />
            <button>Submit</button>
        </form>
    )
}
```

- This pattern moves away from React's declarative way of doing things. 
- The `Form` component above is referred to as an *uncontrolled component* because it uses the DOM to store form state.
- In a *controlled component*, form state is managed by React. The imperative approach above can be re-written declaratively using `useState`. This approach creates two-way data binding.

> [!note]
> Controlled components are re-rendered frequently because of updates made on every change event.

```jsx
const Form = () => {
    const [text, setText] = useState("")

    const submit = (e) => {
        e.preventDefault()
        console.log(text)
        setText("")
    }

    return (
        <form onSubmit={submit}>
            <input value={text} onChange={e => setText(e.target.value)} />
            <button>Submit</button>
        </form>
    )
}
```

- We can abstract away this process using custom hooks for reuse on other input elements.

```jsx
const useInput = initValue => {
    const [value, setValue] = useState(initValue)

    return [
        {
            value,
            onChange: e => setValue(e.target.value)
        },
        () => setValue(initValue)
    ]
}

const Form = () => {
    const [textProps, resetText] = useInput("")

    const submit = (e) => {
        e.preventDefault()
        console.log(textProps.value)
        resetText()
    }

    return (
        <form onSubmit={submit}>
            <input {...textProps} />
            <button>Submit</button>
        </form>
    )
}
```

> [!important]
> When using this approach with text input fields (`<input />` and `<textarea>`), setting an initial state (`""`) is important. 

- For other types of form controls such as radio buttons and checkboxes, state is bound to the `checked` attribute, but working with them can be more complex.

- Popular Form Libraries
    - Formik
    - React Hook Form
    - TanStack Form

- 📄 **Read More**: [Data Binding in React](https://www.joshwcomeau.com/react/data-binding/)

## Routing

- React Router is the most popular client-side routing library for React.
    - It works by creating a mapping of a path (e.g. `/home`) to an element or a component (e.g. `<HomePage />`)
    - Once routes are defined, we can use the `<Link>` component from React Router for client-side navigation.
    - We can add an `errorElement` property to overwrite the default error pages.

```jsx
import { createBrowserRouter, RouterProvider } from "react-router-dom"
import HomePage from "./views/Home"
import UsersPage from "./views/Users"

const router = createBrowserRouter({
    { path: "/", element: <HomePage /> }
    { path: "/users", element: <UsersPage /> }
})

const App = () => {
    return <RouterProvider router={router} />
}

export default App
```

```jsx
import { Link } from "react-router-dom"

const HomePage = () => {
    return (
        <>
            <h1>Home</h1>
            <p>Go to <Link to="/users">to the users page</Link>.</p>
        </>
    )
}

export default HomePage
```

- Meta-frameworks such as [[Next.js]] use a file-based routing system.

## Accessibility

- [[Accessibility|Web Accessibility]] is a universal and library-agnostic principle. 
- Following A11y best practices such as using the right element for the right job and using semantic elements helps make the web accessible for everyone.
- There are popular component libraries that provide tools to help build accessible React apps: React Aria, Radix UI, Next UI, etc. These libraries use best practices under the hood to ensure accessibility.
    - Adobe's React Aria provides a set of well-tested, unstyled React components and hooks to build accessible UI components. It provides components for common UI patterns such as switches and calendars.

## Testing

### Unit/E2E Testing

- Popular testing tools:
    - React Testing Library
    - Jest / Vitest
    - Playwright
    - Cypress
    - Enzyme

### Typechecking

#### PropTypes

- Older versions of React had a built-in typechecking library `PropTypes`, which was part of the core library. 
    - It has since been separated from React, and published as an independent library that works in both class-based components and functional components.

```jsx
import PropTypes from 'prop-types';

const User = ({ name, age }) => {
    return (
        <section>
            <h1>Name: { name }</h1>
            <h1>Age: { age }</h1>
        </section>
    );
}

User.propTypes = {
    name: PropTypes.string.isRequired,
    age: PropTypes.number
};
```

#### TypeScript

- [[TypeScript]] is a superset of [[JavaScript]] that offers typechecking. 
- It can be used in React apps to validate prop types as well as values passed into hooks such as `useState`.

```jsx
type Props = {
    name: string;
};

const User = ({ name }: Props) => {
    return (
        <section>
            <h1>Name: { props.name }</h1>
        </section>
    );
}
```

#### Flow 

- Flow is another static typechecking tool that's built by Facebook and offers a similar functionality to TypeScript.

## Miscellany

### Architecture

#### The Component Lifecycle

- Every React component goes thru:
    - **mounting** - gets added to the screen
    - **updating** - receives new prop or state values
    - **unmounting** - gets removed from the screen

![React Component Lifecycle Methods](assets/images/react.component-lifecycle.png)
- **Credit** - [Dan Abramov](https://twitter.com/dan_abramov/status/981712092611989509)

- The ==`componentDidMount()`== method is executed on initial render. 
- The ==`componentDidUpdate()`== lifecycle method is called on every re-render. 
- The ==`componentWillUnmount()`== method is called right before a component is removed from the DOM.

> [!note]
> An effect's 'lifecycle' is different from a component's.

### Design Patterns

#### Higher-Order Components (HOC)

- HOCs are an abstraction over a component. They receive another component as an argument, applies some logic on the component, and return it.
- Common use cases for HOCs include:
    - **Conditional Rendering**
    - **Styling**
    - **Auth**
    - **State Managment**
    - **Memoization**
    - **Handle Data Fetching / Loading Sates**

```jsx
{/* An HOC that handles the loading state for data fetching */}
const withLoader = (Element, url) => {
    return (props) => {
    const [data, setData] = useState(null);

    useEffect(() => {
        async function getData() {
            const res = await fetch(url);
            const data = await res.json();
            
            setData(data);
        }

        getData();
    }, []);

    if (!data) {
        return <div>Loading...</div>;
    }

    return <Element {...props} data={data} />;
  };
}
```

```jsx
export const withThemeContext = Component => (
  props => (
    <ThemeContext.Consumer>
      {context => <Component themeContext={context} {...props} />}
    </ThemeContext.Consumer>
  )
)

const MyComponent = ({ themeContext, ...props }) => {
  themeContext.someFunction()
  return (<div>Hello, React!</div>)
}

export default withThemeContext(MyComponent)
```

#### Effects

- React components need to be [[Pure Functions|pure]]. They shouldn't cause any side-effects.
    - Any form of computation that falls outside of calculating a view based on props ans state is a side-effect.
        - e.g. API calls, using browser APIs such as `setInterval`, manual [[DOM]] manipulation.
- If a side effect is triggered by an event, it should be in an event handler.
- If a side effect is responsible for synchronizing a component with an external system, it should be inside `useEffect`.
    - `useEffect` removes the side effect from the rendering flow, and delays its execution until after rendering is complete.

#### The Provider Pattern

- This pattern can be used to share global data across multiple components in a tree by utilizing a `Provider` component.
    - React's Context API and libraries like React Redux make use of this pattern.

```jsx
import { createContext } from "react";

const Ctx = createContext({});

function User() {
    return (
        <Ctx.Consumer>
            {({ name }) => (<p>{ name }</p>)}
        </Ctx.Consumer>
    );
}

export default function App() {
    return (
        <Ctx.Provider value={{ name: "John Doe" }}>
            <h1>
                Welcome
                <User />
            </h1>
        </Ctx.Provider>
    );
}
```

#### Render Props

- In similar fashion to HOCs, we can use render props to make components reusable.
- Components are passed as props, and get rendered when specific conditions are met.
    - Functions can also be passed as props, and be used as part of the rendering process.
- They are used to increase reusability in async components.

```jsx
function TodoList({ todos=[], emptyList }) {
    if (!todos.length) return emtpyList;

    return <p>{ todos.length } Todos</p>;
}

export default function App() {
    return <TodoList renderEmptyList={<p>No Todos.</p>} />;
}
```

#### Composition vs. Inheritance

![[Composition vs. Inheritance]]

- React recommends using composition over inheritance to reuse code between components. 
- Components in React are just objects, so they can be passed as props like any other data. 
    - This approach similar to '*slots*' in other libraries such as [[Vue.js|Vue]], but there are no limitations on what can be passed as props in React.

### Portals

- Portals in React are a way of rendering elements outside the React hierarchy tree.
- `createPortal` can be used to render a component into a different part of the DOM.

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

### Project Structure

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

## React Best Practices

- Never define a component inside another component.
    - Every component should be defined at the top level in a file.

### Performance

- `React.lazy()` can be used to defer loading a component until it has rendered.

```jsx
const TodoList = React.lazy(() => import("./TodoList"));
```

- The `<Suspense>` component wraps around specific components, and renders a fallback content (e.g. loading message) when lazy loading occurs (i.e. until its children are done loading).

```jsx
export default function App() {
    return (
        <React.Suspense fallback={<p>Loading Todos...</p>}>
            <TodoList />
        </React.Suspense>
    )
}
```

## Legacy

- In former versions of React, it was necessary to import the library in each JSX file.

### `createClass`

- Originally, components were created using the now deprecated `createClass`.

```js
const TodoList = React.createClass({
    displayName: "TodoList",
    render() {
        return React.createElement(
            "ul",
            { className: "todos" },
            this.props.items.map((todo, i) => {
                return React.createElement("li", { key: i }, todo)
            })
        );
    }
});
```
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

> [!note]
> Currently, error boundaries can only be created using class components. But, libraries like `react-error-boundary` can provide the functionality.

#### Typechecking

```jsx
import PropTypes from 'prop-types';

class User extends React.Component {
    render() {
        return (
            <section>
                <h1>Name: {this.props.name}</h1>
                <h1>Age: {this.props.age}</h1>
            </section>
        );
    }
}

User.propTypes = {
    name: PropTypes.string.isRequired,
    age: PropTypes.number
};
```

---
## Keep Learning

- [ ] React Architecture
    - [React: Software Architecture (LinkedIn Learning)](https://www.linkedin.com/learning/react-software-architecture)
    - [React Beyond the Render (Unicorn Utterances)](https://unicorn-utterances.com/collections/react-beyond-the-render)
    - [React Design Patterns (refine)](https://refine.dev/blog/react-design-patterns/)
    - [Introducing React Design Patterns: Flux, Redux, and Context API](https://www.educative.io/blog/react-design-patterns-best-practices)
        - Fiber Architecture
            - State Scheduling and Batching
    - Server Components
        - https://www.joshwcomeau.com/react/server-components/
        - https://servercomponents.dev/
- [ ] React + TypeScript
- [ ] Testing
    - Testing Library / Playwright
- [ ] Animations + Transitions
    - Motion
    - Remotion

---

## Further

### Books 📚

- Learning React (Alex Banks)

### Ecosystem 🏵

> [enaqx/awesome-react (GitHub)](https://github.com/enaqx/awesome-react#readme)

#### Assorted

- Mantine
- SWR
- React Hook Form
- TanStack
- useHooks
- Framer Motion
- Testing Library

#### Meta-frameworks

- Next.js
    - Nextra
- Remix

#### State Manangement

- Redux
    - Redux Toolkit (RTK)
- Zustand

#### UI

- NextUI
- Tailwind CSS
- Radix UI
    - Shadcn-UI
- Chakra UI
- Ant Design
- Mantine
- Material UI
- React Aria
- Panda CSS
- StyleX
- Storefront UI

### Learn 🧠

- [React: The Complete Course - Udemy](https://www.udemy.com/course/react-the-complete-guide-incl-redux/)

- [Learn React](https://react.dev/learn)

- [React 2025 (by Lee Robinson)](https://react2025.com/)

- [React Handbook](https://reacthandbook.dev/)

- [React, visualized (react.gg)](https://react.gg/visualized)

- [The Framework Field Guide (Unicorn Utterances)](https://unicorn-utterances.com/collections/framework-field-guide)

### Reads 📄

- [Why React? (ui.dev)](https://ui.dev/c/react/why-react)

- [A guide to React design patterns (LogRocket)](https://blog.logrocket.com/react-design-patterns/)

- [Data fetching with React Suspense (LogRocket Blog)](https://blog.logrocket.com/data-fetching-react-suspense/)

- [The Interactive Guide to Rendering in React](https://ui.dev/why-react-renders)

- [Common Beginner Mistakes with React](https://www.joshwcomeau.com/react/common-beginner-mistakes/)

- [Protected Routes and Authentication with React Router](https://ui.dev/react-router-protected-routes-authentication)

- [React Architecture: How to Structure and Organize a React Application (Tania Rascia)](https://www.taniarascia.com/react-architecture-directory-structure/)

- [React Design Principles](https://principles.design/examples/reactjs-design-principles)

- [React Tricks: Fast, Fit and Fun](https://molefrog.com/notes/react-tricks)

- [Rendering Patterns](https://www.patterns.dev/posts/rendering-patterns)

- [Tao of React - Software Design, Architecture & Best Practices](https://alexkondov.com/tao-of-react/)

### Resources 🧩

- [enaqx/awesome-react](https://github.com/enaqx/awesome-react#readme)

- [React Patterns](https://www.patterns.dev/react)

- [React TypeScript Cheatsheet](https://react-typescript-cheatsheet.netlify.app/)

### Roadmaps 🗺

- [React Roadmap](https://roadmap.sh/react)