# Assertions

## When to use vs throwing an Exception

Only to help other devs

- documenting your understanding of the code at a point
    - guarantees about
        - inputs (preconditions)
        - program state (invariants)
        - outputs (post-conditions)
        - like CSC494 & contracts

- debugging a broken algo


```python
if condition1:
    pass
else:
    assert False, (
    "This should never happen, but it does sometimes."
    "We're trying to figure out why. Email us if you hit this!")
```

## When to not use assertions

- data processing
- data validation
- error handling

- assertions are usually disabled in prod
    - performance

- don't cause side-effects in assertions

```python
assert treeDepth() == 7;
```