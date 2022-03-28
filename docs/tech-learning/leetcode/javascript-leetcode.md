## Data Structures
### [JavaScript DefaultDict](https://stackoverflow.com/a/44622467/8479344)

```javascript
class DefaultDict {
  constructor(defaultInit) {
    return new Proxy({}, {
      get: (target, name) => name in target ?
        target[name] :
        (target[name] = typeof defaultInit === 'function' ?
          new defaultInit().valueOf() :
          defaultInit)
    })
  }
}

const counts = new DefaultDict(0)
counts.c += 1  // 1

const lists = new DefaultDict(Array)
lists.men.push('bob')
lists.women.push('alice')
console.log(lists.men) // ['bob']
console.log(lists.women) // ['alice']
console.log(lists.nonbinary) // []
```
###  defaultdict with Map in JS

*  in TODO: how do I create a default value for a Map()?? extending it isn't enough
* I need to create a proxy with this???
```javascript
class MapWithDefault extends Map {
  get(key) {
    if (!this.has(key)) this.set(key, this.default());
    return super.get(key);
  }
  
  constructor(defaultFunction, entries) {
    super(entries);
    this.default = defaultFunction;
  }
}

const m = new MapWithDefault(() => 0);
```
