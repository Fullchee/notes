
### Importing a `type` that's the same name as the `class`
When working with `progressbar.js`, I was getting errors

When I tried importing the `Shape`, 

```jsx
import  ProgressBar, { PathDrawingOptions, Shape } from  'progressbar.js';
```

I had to use `typeof Shape` because I was importing the class `Shape` rather than the type


#### Solution

```jsx
import type Shape from 'progressbar.js/shape';
```

```typescript
// @ts-ignore
```

### Object that has at least these two properties



```typescript
<T extends {first: string; last: string}>(obj: T) 
```