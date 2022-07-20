# Lists

## Flatten a list of lists

```python
list(
itertools.
chain.from_iterable([[3,5,7], [0,6], [0, 5, 8]]))
```

lazily get all of the values

```python
def from_iterable(iterables):
    # chain.from_iterable(['ABC', 'DEF']) --> A B C D E F
    for it in iterables:
        for element in it:
            yield element
```

## [Deep copying](https://fullchee.github.io/notes/backend/python/custom-classes/?h=shallow#deep-copying)

## `array.array`

- start off with `list`
- use `array.array` if you run out of space
    - constrained to one type => less space
    - thin wrapper on C arrays
    - typically for interfacing C code
- still a dynamic `list`
    - same operations

```python
from array import array
arr = array('f', (1.0, 1.5))
```

### `array.array` vs `np.array`

- `array.array` is way more lightweight
- `np` does a ton more stuff
    - numerical calc


## Sets

- frozenset
- collections.Counter


```python
>>> loot = {'sword': 1, 'bread': 3}
>>> inventory.update(loot)
>>> inventory
Counter({'bread': 3, 'sword': 1})
>>> more_loot = {'sword': 1, 'apple': 1}
>>> inventory.update(more_loot)
>>> inventory
Counter({'bread': 3, 'sword': 2, 'apple': 1})
```

```python
>>> len(inventory)
3 # Unique elements
>>> sum(inventory.values())
6 # Total no. of elements
```