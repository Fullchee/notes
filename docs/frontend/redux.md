# Redux

## Why Redux

```jsx
import { useSelector, useDispatch } from 'react-redux';
const user = useSelector(state => state.user);

```

```jsx
import { useSelector, useDispatch } from 'react-redux';
const dispatch = useDispatch();

dispatch({
    type: "ACTION_TYPE",
    ...
});

dispatch((dispatch, ))
```