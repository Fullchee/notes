## External tools

### ESLint

```javascript
/* eslint-disable rule-name */

/* eslint-disable-next-line rule-name */

// @ts-ignore
```

### Console API
https://developer.chrome.com/docs/devtools/console/api/
```javascript
console.log("%cMessage", "color: orange; background-color: blue")
```

## Objects

### Destructure 3 levels down

```javascript
myObject?.props?.match
```

If you know the property will exist
```javascript
const {
  props : {
    match
  },
} = myObject;
```

### Default Dict

```javascript
(obj['key'] || obj['key'] = []).push('value')

(obj['key'] || obj['key'] = 0) += 1
```


### [`new` keyword](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new#description)

1. Creates a new object
    2. type: `object`
2. It sets this new object's internal, inaccessible, [[prototype]] (__proto__) property to be the constructor function's external, accessible, prototype object (every function object automatically has a prototype property).
3. Variable points to the newly created object.
4. Executes the constructor function
5. Return the new object
    1. unless the constructor function returns a non-null object reference.
    2. In this case, that object reference is returned instead.

#### [How do you know if they used `new`?](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new.target)

```javascript
function Foo() {
  if (!new.target) { throw 'Foo() must be called with new'; }
}
```

#### Why `Set()` returns an error without `new`

* without the `new`, the constructor will get called as a regular function
* it will use `this` from the caller's context and not from `Set` and it might break


## Arrays

### Only getting the second value in an array

```javascript
[count, setCount];
[, setCount];

```

### Conditional values in an array
```javascript
const arr = [
  flag && value
].filter(Boolean)
```

### [Sorting](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)

mutates the existing array

- Alphabetically
    - `arr.sort()`
- numerically ascending
    - `arr.sort((a, b) => a - b)`


## Strings

### Template Literals

Feels like Python `f"formatted_string"`

```javascript
myTag`A${1}B${2}C${3}D${4}E${5}F`

function myTag(strings, ...args) {
  console.log(strings); // ['A', 'B', 'C', 'D', 'E', 'F']
  console.log(args); // [1,2,3,4,5]
  return strings;
}
```


## Dates
```javascript
date.toLocaleDateString()
```

### Temporal API
