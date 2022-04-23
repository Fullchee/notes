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

### Only getting the second value in an array

```js
[count, setCount];
```

```js
[, setCount];
```


### Conditional values in an array
```javascript
const arr = [
  flag && value
].filter(Boolean)
```

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