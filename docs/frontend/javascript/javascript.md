## External tools

#### Run `prettier` and then `eslint`

```bash
prettier --write src
npm run lint -- --fix
```

### Console API

https://developer.chrome.com/docs/devtools/console/api/

```javascript
console.log("%cMessage", "color: orange; background-color: blue");
```

## Objects

### Destructure 3 levels down

```javascript
match = obj?.props?.match;
```

If you know the property will exist

```javascript
const {
    props: { match },
} = obj;
```

```javascript
const {
    a: {
        b: {c}
    }
} = obj
```

### Default Dict

```javascript
(obj['key'] || obj['key'] = []).push('value')

(obj['key'] || obj['key'] = 0) += 1
```

### [`new` keyword](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new#description)

1. Creates a new object 2. type: `object`
2. It sets this new object's internal, inaccessible, [[prototype]] (**proto**) property to be the constructor function's external, accessible, prototype object (every function object automatically has a prototype property).
3. Variable points to the newly created object.
4. Executes the constructor function
5. Return the new object
    1. unless the constructor function returns a non-null object reference.
    2. In this case, that object reference is returned instead.

#### [How do you know if they used `new`?](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new.target)

```javascript
function Foo() {
    if (!new.target) {
        throw "Foo() must be called with new";
    }
}
```

#### Why `Set()` returns an error without `new`

-   without the `new`, the constructor will get called as a regular function
-   it will use `this` from the caller's context and not from `Set` and it might break

## Arrays

### Only getting the second value in an array

```javascript
[count, setCount];
[, setCount];
```

### Conditional values in an array

```javascript
const arr = [flag && value].filter(Boolean);
```

### 2 arrays: check identical? (same order)

```javascript
Arr1.length === arr2.length && arr1.every((item, i) => arr2[i] === item);
```

### [Sorting](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)

mutates the existing array

-   Alphabetically
    -   `arr.sort()`
-   numerically ascending
    -   `arr.sort((a, b) => a - b)`

## Strings

### Template Literals

Feels like Python `f"formatted_string"`

```javascript
myTag`A${1}B${2}C${3}D${4}E${5}F`;

function myTag(strings, ...args) {
    console.log(strings); // ['A', 'B', 'C', 'D', 'E', 'F']
    console.log(args); // [1,2,3,4,5]
    return strings;
}
```

## Dates

```javascript
date.toLocaleDateString();
```

### Temporal API

## Numbers

### NaN

```javascript
Number.isNaN("a"); // false
isNaN("a"); // true

Number.isNaN(Number(input)) === isNan(input);
```

## Browser

### Sub-resource integrity

```html
<script src="//cdnjs....."
 integrity="sha256-..."
crossorigin="anonymous">
```

if the CDN gets hacked, then the script won't run

### [Get the URL params](https://stackoverflow.com/a/901144/8479344)

```javascript
// ?q=turtles or window.location.search
search_string = new URL("https://www.google.ca/search?q=turtles&oq=tortuga");
search_string = new URL(window.location.search);

params = new URLSearchParams(search_string);

params.get("q"); // "turtles"
```

## Promises

### Promise error handling

#### `Promise.finally` doesn't affect the return value of the function

```javascript
result = getJson()
  .then(data => "data")
  .catch(error => "error")
  .finally(() => "do something")
```
- “result” will either be “data” or “error” if an error is caught


#### Order of `.then()` vs `.catch()`

```js
p.then(fn1).catch(fn2);
```

- `.catch()` catches errors in both the promise and in `fn1`

vs

```js
p.catch(fn2).then(fn1);
```

- `.catch()` only catches errors in the promise
- useful if you want to continue the promise chain and run fn1
    - return in the `catch`
    - re-throw an error to keep the Promise rejected

vs 

```js
p.then(fn1, fn2)
```

- ensures that only one function ever gets called


#### [`Promise.reject()` vs `throw` vs `] (https://stackoverflow.com/questions/33445415/javascript-promises-reject-vs-throw)

- `Promise.reject(new Error())` is the same as `throw new Error()`

```js
async function test() {
  result = await promise1.catch((error) => {
    return Promise.reject("Hi")  // will trigger the second catch
  }).catch(error => {  // 
    console.log(`Second catch: ${error}`)
    return error
  }) 
  console.log(result)
}
```

- if you want to `throw` in an async callback (like `setTimeout`)
    - https://stackoverflow.com/a/33446005/8479344

#### Return value in `.catch()`


```js
Promise.reject(e);
```