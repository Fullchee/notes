## TODOs

-   [Python glossary](https://docs.python.org/3/glossary.html)
-   Keep up to date
    -   [Python Bytes: Python headlines](https://pythonbytes.fm/)

## Functions

### Forced name params

-   pass a `*` to separate positional args and keyword args

```python
def foo(pos, *, forcenamed, **kwargs):
    pass

my_func(1, 2) # throws an error
```


### Mark a function as deprecated

- https://github.com/tantale/deprecated
- decorator

### Trivia

```python
def yell():
    pass

bark = yell

del yell  # only deletes one pointer to the function

bark()  # still in the heap because there's still one pointer left
```

## `breakpoint()`

-   https://www.youtube.com/watch?v=IzgSl-tkPPg
-   `n` next / step over
-   `s` step into
-   `l` list code
-   `j <line>` jump to line
-   `b <line>` or `break <line>` set breakpoint
-   `c` or `continue` until breakpoint
-   `h` help

or start a file with PDB

```bash
python -m pdb file.py
```

## Formatting

-   In the root of the project
    -   Create a file called: `pyproject.toml`
    -   to configure the `Black` formatter

```toml
[tool.black]
include = '^/c1130/.*/*\.py$'
extend-exclude = '/migrations/'
line-length = 120
```

## Enum

```python
class Color(str, Enum):
    GREEN: '#00ff00'

Color.GREEN == '#00ff00'
```

## CLI

-   `python -m module_name args`
    -   run a module
    -   `python -m http.server`
        -   start http server on port 8000 in current directory
    -   `python -m pdb path/to/file.py`
        -   debug a Python script

## File system

### Path

```python
from pathlib import Path

file_directory = Path(__file__).parent.resolve()
another_path = file_directory / "sql_scripts"
```

### Get an environment variable value

```python
os.environ.get('ENV_VAR_NAME', 'FALLBACK_VALUE')
```

### dataclass vs namedtuple

namedtuple is immutable

dataclass is mutable

both can have default values

```python
StatsTup = namedtuple('Stats', ['min', 'max'], defaults = [3, 7])

@dataclass
class Stats:
    min: int = 3
    max: int = 7
```

## Virtual environment

Uninstall all packages in a virtual env

## Equality

### `==` vs `is`

- `is`: same ID
- `==`: uses `__eq__`


### [`isinstance` vs `type()`](https://stackoverflow.com/a/1549854/8479344)

- `type`: returns the name of the type
- `isinstance([1,2,3], list)`
    - goes up the inheritance tree
    - can catch more than comparing two `type`s


### [walrus operator](https://fullchee-reminders.netlify.app/link/1945)

```python
match = MY_REGEX.search(string)
if match:
    pass
```

```python
if match := MY_REGEX.search(string):
    pass
```

```python
while chunk := f.read(8192):
    md5.update(chunk)
```

- new in Python 3.8
- assignment expression
    - merge two lines into one
- assignment statements needs to be on their own line
- **When to use?**
    - only if it makes your code more readable


## Dynamic imports

```python
from importlib import import_module

# like backendcore.path.to.file
if module_path := getattr(settings, "SOME_NAME", None):
    module = import_module(module_path)
    return getattr(module, "DashboardServices")()
return fallback
```