https://docs.python.org/3/library/re.html

[Trey Hunner - Readable Regular Expressions - PyCon 2017](https://www.youtube.com/watch?v=0sOfhhduqks)

Always use raw strings (aka regex strings)

* so that it doesn't escape `"C:\Programs\nathan"`
* `\n` is a newline 😱
* `r"C:\Programs\nathan"`
    * is what we expect 😄

```python
re.search(r"[^0-9]", "100")  # not numeric, only works at the top
re.search(r"[0-9^]"", "100")  # numeric or ^ symbol
```


### [Verbose mode](https://youtu.be/0sOfhhduqks?t=3868)

you can leave comments

```python
def is_valid_uuid(uuid: str) -> bool:
    return bool(re.match(r"""
        ^
        [a-f\d]{8}  # 8 hex digits
        -
        [a-f\d]{4}  # 4 hex digits
        -
        [a-f\d]{4}  # 4 hex digits
        -
        [a-f\d]{4}  # 4 hex digits
        -
        [a-f\d]{12} # 12 hex digits
        $
    """, uuid, re.IGNORECASE | re.VERBOSE))
```

