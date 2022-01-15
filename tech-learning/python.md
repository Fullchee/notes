### [Context Manager](https://realpython.com/python-with-statement/#creating-function-based-context-managers)
Create a function that can be used `with`

```python
    >>> @contextmanager
    ... def hello_context_manager():
    ...     print("Entering the context...")
    ...     yield "Hello, World!"
    ...     print("Leaving the context...")
    ...

    >>> with hello_context_manager() as hello:
    ...     print(hello)
    Entering the context...
    Hello, World!
    Leaving the context...
```

### `debugger` statement

```py
import pdb; pdb.set_trace()

# or
breakpoint()
```

## Testing

### Mock

When using `patch`, you need to set the path to be

- where you're using that function
- not where that function is defined

You can also use `@patch` as a decorator for your test class
```py
@patch("path.where.my_function.is.used", mock_my_function)
class TestStuff(ApiTestCase):
```

## Formatting

- In the root of the project
  - Create a file called: `pyproject.toml`
  - to configure the `Black` formatter

```toml
[tool.black]
include = '^/c1130/.*/*\.py$'
extend-exclude = '/migrations/'
line-length = 120
```

## String formatting
Don't need to escape anymore???
```python
r"D:\Users\path"
```
* raw string