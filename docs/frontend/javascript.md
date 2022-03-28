## TODOs
https://uptodate.frontendrescue.org/

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
