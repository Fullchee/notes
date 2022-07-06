# Assertions

## When to use vs throwing an Exception

- documenting your understanding of the code at a point
    - guarantees about
        - inputs (preconditions)
        - program state (invariants)
        - outputs (post-conditions)
        - like CSC494 & contracts

- debugging a broken algo

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