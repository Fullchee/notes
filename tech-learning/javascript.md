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