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
