# Strings

## String formatting

https://www.pythonmorsels.com/string-formatting/

### `f` strings

### `r`aw strings
-   raw string to ignore
    -   JS has [String.raw](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/raw)

```python
r"D:\Users\path"
```

### Template strings

* less powerful than `f` strings
* useful for (malicious) user input
```python
from string import Template
templ_string = 'Hey $name, there is a $error error!'
Template(templ_string)
    .substitute(
        name=name,
        error=hex(errno))
```


### Nicer multi-line strings

```python
from textwrap import dedent

def copyright():
    print(dedent("""
        Copyright (c) 2022
        All Rights Reserved.
    """).strip("\n"))
```

## Regex

### [`re.match` vs `re.search`](https://stackoverflow.com/a/180993/8479344)

-   `match` at the beginning of the string, or `match` the entire string
    -   faster
-   Otherwise use search
-   both return a match object

```python
re.match("\w+", """something some other thing""")
```
