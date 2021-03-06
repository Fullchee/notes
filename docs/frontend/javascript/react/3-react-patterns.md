# Epic React 3: Advanced React Patterns

Date: 2022-01-02

**Next**

-   4-?

**Back**

-   [[public-foam/epic-react/2-react-hooks]]
-   [[public-foam/epic-react/epic-react]]

-   [Epic React 3: Advanced React Patterns](#epic-react-3-advanced-react-patterns)
    -   [Context Module Pattern](#context-module-pattern)
        -   [Why can't we just put the function in the `useCount` accessor?](#why-cant-we-just-put-the-function-in-the-usecount-accessor)
    -   [Compound components](#compound-components)
        -   [Why do we need to `cloneElement`?](#why-do-we-need-to-cloneelement)
        -   [How do you know if a component is React or a vanilla DOM element?](#how-do-you-know-if-a-component-is-react-or-a-vanilla-dom-element)
        -   [Flexible Compound Components](#flexible-compound-components)
    -   [Prop Collections & Getters](#prop-collections--getters)
    -   [State Reducer](#state-reducer)
        -   [Why is it called State reducer?](#why-is-it-called-state-reducer)
        -   [What does the `={}` do?](#what-does-the--do)
    -   [Control Props](#control-props)
        -   [When to warn?](#when-to-warn)

## Context Module Pattern

-   when creating a `Context` + `useReducer`
-   if you have common dispatches you want to share
    -   just export it from the `counter.js` alongside the `CountProvider` and `useCount`

```js
export { UserProvider, useUser, updateUser };
```

### Why can't we just put the function in the `useCount` accessor?

-   we'd have to add `useCallback` to each function because we'd be putting it in the Provider's `value`
-   won't be able to tree shake (only get the functions we use)
    -   every function would have a `useCallback` because they'd need to be in the dependency array
-   can't lazy load

## Compound components

-   like `Table` and `Column`
-   where `Column` expects a bunch of props from `Table`
    -   but we don't set it explicitly

```js
<Table>
    {/* `Table` gives `Column` some props behind the scenes */}
    <Column />
    <Column />
    <Column />
</Table>
```

### Why do we need to `cloneElement`?

-   state is handled by the parent component
-   we need to clone because we can't modify props directly
    -   like creating a new copy of array
-   we only want to use `cloneElement` on react components
-   Flexible Compound Components uses `Context` so that it can pass to any descendant
    -   so we don't need `cloneElement`

### How do you know if a component is React or a vanilla DOM element?

```
typeof child.type === 'string' // DOM
```

### Flexible Compound Components

-   instead of passing props via `cloneElement`
-   we pass down data via `Context` and `useContext`

## Prop Collections & Getters

Why

-   less duplication
    -   get the shared props
-   example of props to be returned `{'aria-pressed': on, onClick: toggle}`

```js
function useToggle() {
    const [on, setOn] = React.useState(false);
    const toggle = () => setOn(!on);

    function getTogglerProps({ onClick, ...props } = {}) {
        return {
            "aria-pressed": on,
            onClick: callAll(onClick, toggle),
            ...props,
        };
    }

    return {
        on,
        toggle,
        getTogglerProps,
    };
}
```

**Usage**

```js
<Switch {...getTogglerProps({on})} />
<button
  {...getTogglerProps({
    'aria-label': 'custom-button',
    onClick: () => console.info('onButtonClick'),
    id: 'custom-button-id',
  })}
>
```

## State Reducer

-   let the user of the hook pass in their own reducer
    -   inversion of control!
-   to avoid duplication, we can do this to just update one case

```js
function toggleStateReducer(state, action) {
    if (action.type === "toggle" && clickedTooMuch) {
        return { on: state.on };
    }
    return toggleReducer(state, action); // default hook reducer
}
```

### Why is it called State reducer?

-   you pass in a reducer that modifies the state

### What does the `={}` do?

```js
// useToggle() will work
function useToggle({initialOn = false} = {}) {...}
```

vs

```js
// useToggle() will result in an error
function useToggle({initialOn = false}) {
```

## Control Props

-   ![Control Props](/assets/images/blog/sources-tab.png)
-   replicating what React does to forms (controlled vs uncontrolled)
    -   is there a value that tha sh
-   error when going from uncontrolled to controlled (or vice versa)
    -   example: giving React a value and then later assigning it

```js
const on = isControlled ? controlledOn : state.on;

function dispatchWithOnChange(action) {
    if (!isControlled) {
        dispatch(action); // update the redux's state
    }
    const newState = reducer({ ...state, on }, action);
    onChange?.(newState, action);
}
```

### When to warn?

1. Passing `on` without `onChange`
2. Passing a value for `on` and later passing `undefined` or `null`
3. Passing `undefined` or `null` for `on` and later passing a value

console.logs always need to be in a `useEffect`

side effect to check if value is undefined or null

-   `readOnly` prop
-   setting the initial value of `isChange`
-   you can put hooks in the if statement because `process.env.NODE_ENV` never changes

```js
if (process.env.NODE_ENV !== "production") {
    useWarning();
}
```

[//begin]: # "Autogenerated link references for markdown compatibility"
[public-foam/epic-react/2-react-hooks]: ../../epic-react/2-react-hooks "Epic React 2: React Hooks"
[public-foam/epic-react/epic-react]: ../../epic-react/epic-react "epic-react"
[//end]: # "Autogenerated link references"
