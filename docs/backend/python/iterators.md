# Generators and Iterators

## Iterators

### Implementing your own iterator

1. class with an `__iter__`
2. that returns a class with a `__next__`
    3. returns the next item
    4. `StopIteration` exception when it's done

Usually you implement both in the same class and in `__iter__` you return `self`

```python
class BoundedRepeater:
    def __init__(self, value, max_repeats):
        self.count = 0
        self.value = value
        self.max_repeats = max_repeats

    def __iter__(self):
        return self  # don't set the count to 0, just create another BoundedRepeater

    def __next__(self):
        if self.count > self.max_repeats:
            raise StopIteration  # no import, it's a built-in
        self.count += 1
        return value
```

### Implementing a `for` loop with a `while` loop

```python
repeater = BoundedRepeater('Hello', 3)
for value in repeater:
    print(value)
```

```python
repeater = iter(BoundedRepeater('Hello', 3))

while True:
    try:
        value = next(repeater)
    except StopIteration:
        break
    print(value)
```


## [Generator Function](https://www.pythonmorsels.com/what-is-a-generator-function/?watch)

### `yield`

- `yield` an intermediate value
- give control back to the caller
    - doesn't destroy the function stack, just moves the pointer back to the parent
- functions with a `yield` will return a generator

- Just-In-Time version of iterators
- can be a function (no need for a class!)
- optionally
    - `return` to return the final value

```python
def repeater(value, max_repeats):
    for i in range(max_repeats):
        yield value
    # `return` to return the final value
```
- no need to explicitly `raise StopIteration`

**equivalent generator expression**

```python
(value for _ in range(max_repeats))
```

### [Is `range` a generator?](https://stackoverflow.com/a/13092317/8479344)

- https://treyhunner.com/2018/02/python-range-is-not-an-iterator

- nope
- `range` is still lazy though!

> `range` is class of immutable iterable objects

- you can get an iterator from it with `iter(range(1))`
- can't call `next()` directly on `range`
    - `next(range(1))`


## [Generator Expressions](https://www.pythonmorsels.com/how-write-generator-expression/?watch)

### Generator expression vs list comprehensions

#### Syntax

- list comprehension: `[n**2 for n in [1,2,3] if x % 2 == 0] `
- generator expression: `(n**2 for n in [1,2,3] if x % 2 == 0)`


#### Differences
- lazy versions of list comprehensions
- can only loop through once

#### When to use generator expressions
- you only need to go through once
- the list is massive
    - generator expressions have no problem with that
- if you want to break and then come back later


### Generator Chains

- lazily generates one at a time!
- Python doesn't have a built-in compose operator 😞

```python
even_squares = lambda numbers: (n**2 for n in numbers if n % 2 == 0)
negated = lambda numbers: (-n for n in numbers)

chain = negated(even_squares(range(8)))
>> next(chain)
0
>> next(chain)
-4
```

