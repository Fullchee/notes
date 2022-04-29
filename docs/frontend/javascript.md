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


### `new` keyword

1. Creates an empty object
2. Sets the prototype
3. calls the constructor
    4. sets this???
5. returns the constructor return value or the object

#### Why `Set()` returns an error without `new`

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