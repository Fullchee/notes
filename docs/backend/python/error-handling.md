## Error handling

[`logging.warning` vs `warnings.warn`](https://stackoverflow.com/questions/9595009/warnings-warn-vs-logging-warning/14762106#14762106)

-   `logging.warning`
    -   issue with input/user
    -   nothing the client app can do
-   `warnings.warn`
    -   dev issue
        -   deprecated code
        -   abstract class not implement

## [Context Manager](https://realpython.com/python-with-statement/#creating-function-based-context-managers)

### Create your own context manager


```python
with open('hello.txt', 'w') as f:
    f.write('hello')
```


```python
f = open('hello.txt', 'w')
try:
    f.write('hello')
finally:
    f.close()
```

#### Create your own class

- implement `__enter__` and `__exit__`

```py
class ManagedFile:
    def __init__(self, name):
        self.name = name
    def __enter__(self):
        self.file = open(self.name, 'w')
        return self.file  # the return value; ManagedFile() as f
    def __exit__(self, exception_type, exception_value, exception_traceback):
        if self.file:
            self.file.close()
```

```python
with ManagedFile('hello.txt') as f:
    f.write('hello')
```

#### Using the `contextmanager` generator

```python
from contextlib import contextmanager

@contextmanager
def managed_file(name):
    try:
        f = open(name, 'w')
        yield f  # gives f back to the caller, then can do f.write('hello')
    finally:
        f.close()
```


## [`suppress`](https://docs.python.org/3/library/contextlib.html#contextlib.suppress)

Cleaner version of `try/except` and ignore

```python
from contextlib import suppress

with suppress(FileNotFoundError):
    os.remove('somefile.tmp')
```
same as

```python
try:
    os.remove('somefile.tmp')
except FileNotFoundError:
    pass
```




## Exercises

### Python Tricks Page 33

```python
with Indenter() as indent:
    indent.print('hi!')
    with indent:
        indent.print('hello')
        with indent:
            indent.print('bonjour')
    indent.print('hey')
```

Should give

```python
hi!
    hello
        bonjour
hey
```

```python
class Indenter:
    def __init__(self):
        self.indents = -1
    def __enter__(self):
        self.indents += 1
        return self
    def __exit__(self, exception_type, exception_value, exception_traceback):
        self.indents -= 1
    def print(self, string):
        tab = "\t"
        print(f'{tab * self.indents}{string}')
```


### Python Tricks Page 35
- context manager that measures the execution time of a code block using the `time.time` function