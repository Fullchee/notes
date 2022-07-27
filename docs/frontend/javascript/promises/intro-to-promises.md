# Intro to Promises

## How the event loop works
<iframe
  width="713"
  height="360"
  src="https://www.youtube.com/embed/8aGhZQkoFbQ"
  title="What the heck is the event loop anyway? | Philip Roberts | JSConf EU"
  frameborder="0"
  allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
  allowfullscreen
></iframe>


## Callbacks

### Why callbacks?

- execute code after something else finishes


### Example

```js
function printContents(err, data) {
    if (err) {
        console.error(err);
    }
    console.log(data);
}

fs.readFile('package.json', 'utf8', printContents);
```

### Problem with callbacks: Callback hell

```javascript
const fs = require('fs');

fs.readFile('package.json', 'utf8' function(err, data) {
    if (err) {
        console.error(err);
    }
    console.log(data)
    fs.readFile('file2', 'utf8' function(err, data) {
        if (err) {
            console.error(err);
        }
        fs.readFile('file3', 'utf8' function(err, data) {
            if (err) {
                console.error(err);
            }
            fs.readFile('file4', 'utf8' function(err, data) {
                if (err) {
                    console.error(err);
                }
                fs.readFile('file5', 'utf8' function(err, data) {
                    if (err) {
                        console.error(err);
                    }
                    fs.readFile('file6', 'utf8' function(err, data) {
                        if (err) {
                            console.error(err);
                        }
                        fs.readFile('file7', 'utf8' function(err, data) {
                            if (err) {
                                console.error(err);
                            }
                            fs.readFile('file8', 'utf8' function(err, data) {
                                if (err) {
                                    console.error(err);
                                }
                            });
                        });
                    });
                });
            });
        });
    });
});
```

## Promises

### `.then()` example

```js
let file1;
file8Promise = fs.readFile('file1', 'utf8')
    .then(function(_file1) {
        // NOTE: you NEED to return in order for the data to get passed into the function
        file1 = _file1
        return fs.readFile('file2', 'utf8');
    })
    .then(function(file2) {
        console.log(file1);
        console.log(_file1);  // errors out
        return fs.readFile('file3', 'utf8');
    })
    .then(function(file3) {
        return fs.readFile('file4', 'utf8');
    })
    .then(function(file4) {
        return fs.readFile('file5', 'utf8');
    })
    .then(function(file5) {
        return fs.readFile('file6', 'utf8');
    })
    .then(function(file6) {
        return fs.readFile('file7', 'utf8');
    })
    .then(function(file7) {
        return fs.readFile('file8', 'utf8');
    })
    .catch(function() {
        // if any of the 8 error out
        console.error(err);
    });
```

### async/await

```javascript
async function readFiles() {
  try {
    const file1 = await fs.readFile("file1", "utf8");
    const file2 = await fs.readFile("file2", "utf8");
    console.log(file1)
    const file3 = await fs.readFile("file3", "utf8");
    const file4 = await fs.readFile("file4", "utf8");
    const file5 = await fs.readFile("file5", "utf8");
    const file6 = await fs.readFile("file6", "utf8");
    const file7 = await fs.readFile("file7", "utf8");
    const file8 = await fs.readFile("file8", "utf8");
  } catch (error) {
    console.error(error);
  }
}
```

#### Using `useEffect` with `async/await`

- `useEffect` can only return a cleanup function
- need a wrapper

```jsx
useEffect(() => {
    const make_api_call = async () => {
        const response = await fetch()
        const data = await response.json()
    }
    make_api_call()
})
```


### What is a promise

#### My definition

- magic box
- call `.then()` or `await`
    - it'll return the value
    - or throw an error


One of 3 states

- `pending`
- `fulfilled`
- `rejected`
