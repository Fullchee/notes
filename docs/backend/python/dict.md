# Python Dictionaries

## [Deep copying](https://fullchee.github.io/notes/backend/python/custom-classes/?h=shallow#deep-copying)

## Nested get

```python
example_dict.get('key1', {}).get('key2')
```

- default fallback for `.get` is `None`
    - unlike `getattr`
    - which you have to explicitly provide a fallback

## `defaultdict`

```python
my_dict = collections.defaultdict(int)  # default value: 0
my_dict[key] += 1
```

## Get the key with the max value in the dict

```python
stats = {'a': 1, 'b': 3000, 'c': 0}
max(stats, key=stats.get)  # 'b'

max(stats, key=lambda key: stats[key])  # 'b'
```

## [ChainMap](https://florimond.dev/en/posts/2018/07/a-practical-usage-of-chainmap-in-python/#example-the-shopping-inventory)

### Maintaining a precedence chain of defaults

```python
cli_args = {"debug": True}
defaults = {"debug": False}

config = ChainMap(cli_args, defaults)
config["debug"]  # True

# looks for the key in cli_args and then in defaults
```

##  `MappingProxyType`

- read-only immutable dictionaries
- not hashable
    - unlike `namedtuple`
- example
    - dict of internal state that you don't 

```python
from types import MappingProxyType
writable = {'one': 1, 'two': 2}
read_only = MappingProxyType(writable)

>>> read_only['one']
1
>>> read_only['one'] = 23
TypeError:
"'mappingproxy' object does not support item assignment"
# Updates to the original are reflected in the proxy:
>>> writable['one'] = 42
>>> read_only
mappingproxy({'one': 42, 'two': 2})
```

## [UserDict](https://realpython.com/python-collections-module/#customizing-built-ins-userstring-userlist-and-userdict)

When you want to modify the behavior of the built-in dict???
