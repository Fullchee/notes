# Custom classes

## Copying

### Deep copying

```python
import copy
deep_copy = copy.deepcopy([[1,2,3], [4,5,6])
```

### Shallow copying

```python
list([[1,2,3], [4,5,6]])
```

Works on custom classes too!

- Python Tricks ch 4.4
- you can implement `__copy__()` and `__deepcopy__()` for custom behaviour
