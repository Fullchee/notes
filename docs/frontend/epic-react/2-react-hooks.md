# Epic React 2: React Hooks

Date: 2021-12-26

- [Epic React 2: React Hooks](#epic-react-2-react-hooks)
  - [Why React Hooks?](#why-react-hooks)
  - [useState](#usestate)
    - [Why we need useState](#why-we-need-usestate)
  - [useEffect](#useeffect)
    - [Error Boundaries](#error-boundaries)
  - [Advanced React Hooks](#advanced-react-hooks)
  - [useReducer](#usereducer)
  - [useCallback and useMemo](#usecallback-and-usememo)
    - [useCallback: Custom hooks](#usecallback-custom-hooks)
      - [what's the `run` function that we return in `useAsync`?](#whats-the-run-function-that-we-return-in-useasync)
    - [safeDispatch (safe fetch) and useEffect cleanup](#safedispatch-safe-fetch-and-useeffect-cleanup)
      - [How do you know if a component has been unmounted?](#how-do-you-know-if-a-component-has-been-unmounted)
  - [`useContext`](#usecontext)
      - [`useCount` wrapper for better errors](#usecount-wrapper-for-better-errors)
  - [`useEffect` vs `useLayoutEffect`](#useeffect-vs-uselayouteffect)
  - [`useImperativeHandle`](#useimperativehandle)
    - [`React.forwardRef`](#reactforwardref)
    - [Do you need to always use `useImperativeHandle` when using `React.forwardRef`?](#do-you-need-to-always-use-useimperativehandle-when-using-reactforwardref)
    - [`useDebugValue`](#usedebugvalue)

## Why React Hooks?

-   no duplicate code in different lifecycle methods
-   Solves the problem of switching between functional component to class component
-   [Tyler McGinnis: Why React Hooks (the history)](https://www.youtube.com/watch?v=3hCge6XFju8)

## useState

-   accepts a function which is a lazy initializer!
    -   `useState` ignores the param afterward
    -   for computationally expensive stuff (async like )

### Why we need useState

-   we need to re-render the component again

## useEffect

-   dependency array does a `===` comparison
    -   will always re-render if you pass it an array
-   `fetch`: forgot to return early if `pokemonName` is null
-   I forgot about having a status variable
    -   helps with determining what to display
    -   https://kentcdodds.com/blog/stop-using-isloading-booleans
-   the way that Kent does a sort of manual TDD where he always gets something to display
    -   eg: create a variable with a stub error message to make sure that the error shows up

### Error Boundaries

-   can take in a `FallbackComponent` arg
-   Problem with using the `key` prop for the error boundary
    -   it'll mount and unmount every time the `key` is updated
    -   flashing
-   we can pass `resetErrorBoundary` prop that gets triggered in the `FallbackComponent`
-   `resetKeys` prop works as well

## Advanced React Hooks

Custom hooks are just regular functions that happen to have side effects!

They can return anything

## `useReducer`

```jsx
function reducer(state, action) { ... }

const [state, dispatch] = useReducer(reducer, initialValue);

dispatch(action)
```

-   doesn't have to follow the Redux style of having actions with a `type` prop
-   first prop: the old state
-   second prop: whatever you pass to `dispatch`
    -   usually `action`

### Implementing `useState` with `useReducer`
```jsx
const [count, setCount] = useState(0);
```

```jsx
function countReducer(state, newState) {
  return newState;
}

const [count, setCount] = useReducer(0);
setCount(1);
```


### useReducer vs useState

- useReducer might be good for more complex logic

## useCallback and useMemo

Use cases (https://kentcdodds.com/blog/usememo-and-usecallback)

1. not have a function re-render every time so that it can be used in a useEffect dep array
2. avoiding unnecessary re-renders when re-rendering is super expensive (Graphs, Charts, Animations)
3. `useMemo` can be passed a function (just like `useState`) and lazily calculate computationally expensive items 4. I used it in `HierarchySelect` where there was derived state that wasn't updated often

### useCallback: Custom hooks

-   I had trouble with the middle param of what the initial state should be
-   I autofilled the dependencies and got into an infinite render loop

#### what's the `run` function that we return in `useAsync`?

-   instead of the user putting their `fetch` in a `useCallback`
-   the `useEffect` in `useAsync` becomes `run` which is memoized with `useCallback`
-   they can put it in a `useEffect` and `run(result)`

### safeDispatch (safe fetch) and useEffect cleanup

-   Memory leak when unmounting before the `fetch` finishes
-   it's not a class component so we can't just have a `componentWillMount` and abort the `fetch`
-   I have to cancel subscriptions and async tasks in the useEffect cleanup function

#### How do you know if a component has been unmounted?

```jsx
React.useLayoutEffect(() => {
    mountedRef.current = true;
    return () => {
        mountedRef.current = false;
    };
}, []);
```

-   https://github.com/helderburato/use-is-mounted-ref/blob/main/src/use-is-mounted-ref.ts

## `useContext`

-   Always give your contexts a `display name`
    -   `ToggleContext.displayName = 'ToggleContext'`
    -   shows up in the browser dev tools
-   creating a `CountProvider` component wrapper
    -   so that it can have its own state and hooks to manage the state
    -   instead of directly using `<ToggleContext.Provider value={{count, setCount}}>...</...>`
-   you can pass `count` and `setCount` as the value of the Provider

#### `useCount` wrapper for better errors

```js
const value = React.useContext(CountContext);
if (!value) {
    throw new Error("useState must be within the CountContext");
}
return value;
```

## `useEffect` vs `useLayoutEffect`

-   same API
-   useEffect is run after pixels are painted
-   useLayoutEffect is run before so it will delay painting
    -   can update the DOM before it paints

## `useImperativeHandle`

-   ????

### `React.forwardRef`

-   can pass a `ref` as a second param
    -   instead of the first param with all the other regular props

**Could you put `ref` as a prop? in the first param of the component?**

-   yeah but that would cause a re-render
-   you might not want to always re-render when the ref that's passed down to the component changes

### Do you need to always use `useImperativeHandle` when using `React.forwardRef`?

### `useDebugValue`

-   feels like `__repr__` in Python for custom hooks
