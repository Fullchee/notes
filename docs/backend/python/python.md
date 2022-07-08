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

## Strings

### String formatting

https://www.pythonmorsels.com/string-formatting/

-   raw string to ignore
    -   JS has [String.raw](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/raw)

```python
r"D:\Users\path"
```

#### Nicer multi-line strings

```python
from textwrap import dedent

def copyright():
    print(dedent("""
        Copyright (c) 2022
        All Rights Reserved.
    """).strip("\n"))
```

### Regex

#### [`re.match` vs `re.search`](https://stackoverflow.com/a/180993/8479344)

-   `match` at the beginning of the string, or `match` the entire string
    -   faster
-   Otherwise use search
-   both return a match object

```python
re.match("\w+", """something some other thing""")
```

## Typing

[`obj.attribute` vs `obj["member_of_collection"]`](https://stackoverflow.com/questions/30250282/whats-the-difference-between-the-square-bracket-and-dot-notations-in-python)

[Property vs attribute](https://stackoverflow.com/questions/7374748/whats-the-difference-between-a-python-property-and-attribute)

-   property is a special kind of attribute
    -   has either a `__get__`, `__set__` or `__delete__`
    -   `spam.eggs` will return the result of `__get__`

```python
spam = SomeObject()
print(spam.eggs)
```

### TypedDict

-   new in Python 3.8
-   https://adamj.eu/tech/2021/05/10/python-type-hints-how-to-use-typeddict/

```python
from typing import TypedDict


class SalesSummary(TypedDict):
    sales: int
    year: NotRequired[int]
    product_codes: list[str]

def get_sales_summary() -> SalesSummary:
    pass
```

### [Circular Dependencies with types](https://www.youtube.com/watch?v=UnKa_t-M_kM&t=213s)

```python
from __future__ import annotations
from typing import TYPE_CHECKING # false at runtime

if TYPE_CHECKING:
    from module_b import B
```

## Dynamic Imports

- 

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

## Lists

### Flatten a list of lists

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