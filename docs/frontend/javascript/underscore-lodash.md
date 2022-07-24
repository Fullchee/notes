## Underscore

**Playground**

https://stackblitz.com/edit/underscore-playground


```javascript
var stooges = [{name: 'curly', age: 25}, {name: 'moe', age: 21}, {name: 'larry', age: 23}];
```

### `_.chain`

```javascript
var sorted = _.sortBy(stooges, stooge => stooge.age)
var formatted = _.map(sorted, stooge => `${stooge.name} is ${stooge.age}`)
var first = _.first(formatted)
```

Allows you to chain (like vanilla JS)

```javascript
var youngest = _.chain(stooges)
  .sortBy(function(stooge){ return stooge.age; })
  .map(function(stooge){ return stooge.name + ' is ' + stooge.age; })
  .first()
  .value();
```

Note that you need the `.value()` after

Problem with `_.chain`

* it imports all of `underscore`


### [`_.groupby`](https://underscorejs.org/#groupBy)

```javascript
_.groupBy([1.3, 2.1, 2.4], function(num){ return Math.floor(num); });
=> {1: [1.3], 2: [2.1, 2.4]}

_.groupBy(['one', 'two', 'three'], 'length');
=> {3: ["one", "two"], 5: ["three"]}
```
