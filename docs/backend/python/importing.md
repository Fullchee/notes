# Imports

## Dynamic imports

- lazy loading
- in backend-core, import the corresponding client module
    - defined in Django settings

```python
from importlib import import_module

module = import_module("module_name")

# example
module = import_module(settings.DASHBOARD_SERVICES)
```


## Trivia

```python
from my_module import *  # won't include _fn_name
from my_module import _fn_name  # this works
```

- it won't import `_fn_name()`
    - unless there's an `__all__ = ["_fn_name"]`

you really shouldn't use wildcard `*`

