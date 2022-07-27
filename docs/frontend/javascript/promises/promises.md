# Non-intro Promise Notes

## Promise error handling

### `Promise.finally` doesn't affect the return value of the function

```javascript
result = getJson()
  .then(data => "data")
  .catch(error => "error")
  .finally(() => "do something")
```
- “result” will either be “data” or “error” if an error is caught


### Order of `.then()` vs `.catch()`

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


### [`Promise.reject()` vs `throw`] (https://stackoverflow.com/questions/33445415/javascript-promises-reject-vs-throw)

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

### Return value in `.catch()`


```js
Promise.reject(e);
```