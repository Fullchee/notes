## Comments

- ignore a rule for the whole file
```javascript
/* eslint-disable rule-name */
// @ts-nocheck (ignores the whole file)
```

- ignore the rule for one line

```javascript
/* eslint-disable-next-line rule-name */

// @ts-ignore (ignores one line)
```

## Empty Types

- `unknown`
    - I don't know
        - could be anything
    - need to type check/guard
- `any`
    - I don't care

### `never`

things that should never happen

- prune conditional types

```ts
type NonNullable<T> = T extends null | undefined ? never : T;

// NonNullable<MyType> can't be assigned null or undefined
```

- infinite loops
- only ever throwing errors


## Checking types

### [`instanceof` vs `typeof`](https://stackoverflow.com/a/6625960/8479344)

JS built-ins

- `instanceof` for custom types
- `typeof` for the simple built-in types


### Type guards

Return type isn't a boolean!

```ts
function isFish(pet: Fish | Bird): pet is Fish {
  return (pet as Fish).swim !== undefined;
}
```

## Type Generation

- [MakeTypes](https://jvilk.com/MakeTypes/)
    - Generates interfaces from JSON
- https://github.com/swagger-api/swagger-codegen


## Interfaces

Extend a type

```ts
interface LoadingWidgets {
    [widgetId?: number]: boolean;
}

interface IsLoading {
    widgets: LoadingWidgets;
    [key?: string]: boolean | LoadingWidgets;
}
```

### [`interface` vs `type`](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#differences-between-type-aliases-and-interfaces)

- both are good, for consistency, stick with one

#### What only `interface` can do

- declaration merging
- interfaces can be changed after being created

```ts
interface Point { x: number; }
interface Point { y: number; }
//becomes: interface Point { x: number; y: number; }
```

#### What only `type` can do

- primitives
    - `#!ts type Name = string`
- unions
    - `#!ts type Id = string | number`
- tuples
    - `#!ts type Data = [number, string]`


## React and TS

### Return type

`JSX.Element` or `ReactElement`?

ReactElement works for an array of functions

## Functions

```typescript
type GreetFunction = (a: string) => void;
```

### Click event

```typescript
(event: React.MouseEvent<HTMLElement>) => void
```

### Importing a `type` that's the same name as the `class`

When working with `progressbar.js`, I was getting errors

When I tried importing the `Shape`,

```jsx
import ProgressBar, { PathDrawingOptions, Shape } from "progressbar.js";
```

I had to use `typeof Shape` because I was importing the class `Shape` rather than the type

#### Solution

There's a separate import for the `Shape`

```jsx
import type Shape from "progressbar.js/shape";
```

```typescript
// @ts-ignore
```

### Object that has at least these two properties

```typescript
<T extends {first: string; last: string}>(obj: T)
```

```typescript
/**
 * Make all properties in T optional
 */
type Partial<T> = {
    [P in keyof T]?: T[P];
};
```

```typescript
/**
 * Make all properties in T required
 */
type Required<T> = {
    [P in keyof T]-?: T[P];
};
```
