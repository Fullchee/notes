## TODOs
* Testing: check out `pytest` and see why some people like it more than `unittest`
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

## Testing


### mock.patch
* `patch` WHERE IT'S USED, not where it's defined
    * the fiile only knows about what files are exported
    * https://youtu.be/ww1UsGZV8fQ?t=434
* 3 ways of patching
    * https://www.youtube.com/watch?v=WFRljVPHrkE

```py
@patch("path.where.my_function", autospec=True, spec_set=True)
class TestStuff(ApiTestCase):
    def test_stuff(self, mock_my_function):
```


#### [Patch Arguments](https://youtu.be/ww1UsGZV8fQ?t=1164)
* `spec`: doesn't know about attributes of attributes
    * should always at least `spec`
* `autospec` doesn't know about dynamically created attributes
    * example: class attributes
    * work around: set the attribute that exists
    * can be dangerous because it can trigger code on introspection
    * can slow down tests
* `spec_set=True` prevent setting properties that don't exist
* `new_callable=MagicMock`is the default
    * `new_callable=PropertyMock`
* kwargs
    * `return_value="lisa"
    * `name="lisa"`
* `patch.object`
* `patch.dict`
* `patch.multiple`

* https://youtu.be/ww1UsGZV8fQ?t=889
```diff
-@patch("path.where.fn1")
-@patch("path.where.fn2")
-@patch("path.where.fn3")
class TestStuff(ApiTestCase):
+    def setUp(self):
+        mock_fn1 = patch("path.where_fn1").start()
+        mock_fn2 = patch("path.where_fn2").start()
+        mock_fn3 = patch("path.where_fn3").start()
+        self.addCleanup(patch.stopall)
-    def test_stuff(self, mock_fn1, mock_fn2, mock_fn3):
+    def test_stuff(self):
        ...
-    def test_stuff2(self, mock_fn1, mock_fn2, mock_fn3):
+    def test_stuff2(self):
        ...
```

* You need `mock_check_output` beacuse the decorator adds it
    * what does it do???????????

patch for as little as possible, especially for 

or use setUp() and tearDown()

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

### String formatting
Don't need to escape anymore???
```python
r"D:\Users\path"
```
* raw string


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

## CLI
* `python -m module_name args`
    * run a module
    * `python -m http.server`
        * start http server on port 8000 in current directory
    * `python -m pdb path/to/file.py`
        * debug a Python script
* 