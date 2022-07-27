# Python Dictionaries

## `dict`

### [Deep copying](https://fullchee.github.io/notes/backend/python/custom-classes/?h=shallow#deep-copying)

### Nested get

```python
example_dict.get('key1', {}).get('key2')
```

- default fallback for `.get` is `None`
    - unlike `getattr`
    - which you have to explicitly provide a fallback

### [Destructure dicts](https://stackoverflow.com/a/52083390/8479344)

In JS

```javascript
params = {a: 1, b: 2};
const {a, b} = params;
```

Python can't do the same thing 😞

Given `#!py params = {'a': 1, 'b': 2}`

**itemgetter**

```python
from operator import itemgetter
a, b = itemgetter('a', 'b')(params)
```

**list comprehension**

```python
a, b = [d[k] for k in ('a','b')]
```

**assignment**

```python
a, b = params['a'], params['b']
```

### key with the max value

```python
d = {'a': 1, 'b': 3000, 'c': 0}
max(stats, key=d.get)  # 'b'

max(stats, key=lambda key: d[key])  # 'b'
```

### Sorting keys

- Python 3.6+: sorted by insertion order
- to sort, convert to to `dict_items`
    - an iterator (kinda like a list of tuples)

```python
>>> d.items()
dict_items([('a', 1), ('b', 3000), ('c', 0)])
```

```python
>>> sorted(d.items(), key=lambda x: x[1])
[('c', 0), ('a', 1), ('b', 3000)]
```

same as

```python
import operator
>>> sorted(d.items(), key=operator.itemgetter(1))
[('c', 0), ('a', 1), ('b', 3000)]
```
### The Craziest Dict Expression

```python
>>> {True: 'yes', 1: 'no', 1.0: 'maybe'}
{True: 'maybe'}
```

- `bool` is implemented as a special int
    - `True == 1 == 1.0`
    - `hash(True) == hash(1) == hash(1.0)`
- dict is looking for a key that matches the same 
    - `__hash__`
    - `__eq__`
- so it overrides the value
- keeps `True` as the key because that was the first key
    - no point in updating the key's representation if it's gonna be the same


## `defaultdict`

```python
my_dict = collections.defaultdict(int)  # default value: 0
my_dict[key] += 1
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
