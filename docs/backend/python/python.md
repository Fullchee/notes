## TODOs
* [Python glossary](https://docs.python.org/3/glossary.html)
* Keep up to date
    * [Python Bytes: Python headlines](https://pythonbytes.fm/)

## Functions
### Forced name params
* pass a `*` to separate positional args and keyword args
```python
def foo(pos, *, forcenamed, **kwargs):
    pass

my_func(1, 2) # throws an error
```


## [Context Manager](https://realpython.com/python-with-statement/#creating-function-based-context-managers)
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

## `breakpoint()`
* https://www.youtube.com/watch?v=IzgSl-tkPPg
* `n` next / step over
* `s` step into
* `l` list code
* `j <line>` jump to line
* `b <line>` or `break <line>` set breakpoint
* `c` or `continue` until breakpoint
* `h` help

or start a file with PDB

```bash
python -m pdb file.py
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

## Strings

### String formatting

https://www.pythonmorsels.com/string-formatting/

* raw string so that you 

```python
r"D:\Users\path"
```
* raw string

### Regex

#### [`re.match` vs `re.search`](https://stackoverflow.com/a/180993/8479344)

* `match` at the beginning of the string, or `match` the entire string
    * faster
* Otherwise use search
* both return a match object

```python
re.match("\w+", """something some other thing""")
```

## Typing

### TypedDict
* https://adamj.eu/tech/2021/05/10/python-type-hints-how-to-use-typeddict/
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

## Enum
```python
class Color(str, Enum):
    GREEN: '#00ff00'
    
Color.GREEN == '#00ff00'
```

## CLI
* `python -m module_name args`
    * run a module
    * `python -m http.server`
        * start http server on port 8000 in current directory
    * `python -m pdb path/to/file.py`
        * debug a Python script



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

## Dict


Get the key with the max value in the dict
```python
stats = {'a': 1, 'b': 3000, 'c': 0}
max(stats, key=stats.get)  # 'b'

max(stats, key=lambda key: stats[key])  # 'b'
```