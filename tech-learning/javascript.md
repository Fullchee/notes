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