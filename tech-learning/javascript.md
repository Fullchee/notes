### Destructure 3 levels down

```javascript
myObject.props.match
```
```javascript
const {  
  props : {  
    match  
  },  
} = myObject;
```

If it gets too complex, use a safe helper

#### How do you safely check?


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