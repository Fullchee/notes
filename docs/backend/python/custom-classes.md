# Custom classes

## Copying

### Deep copying

```python
import copy
deep_copy = copy.deepcopy([[1,2,3], [4,5,6])
```

### Shallow copying

```python
list([[1,2,3], [4,5,6]])
```

Works on custom classes too!

- Python Tricks ch 4.4
- you can implement `__copy__()` and `__deepcopy__()` for custom behaviour

## `namedtuple`

## namedtuple API

- always starts with `_` prefix to avoid conflicts with arbitrarily user defined fields

### Converted namedtuple to dict

```python
my_car._asdict()
OrderedDict([('color', 'red'), ('mileage', 3812.4)])

json.dumps(my_car._asdict())
'{"color": "red", "mileage": 3812.4}'
```

### Extending a `namedtuple` with `_fields`

```python
Car = namedtuple('Car', 'color mileage')
ElectricCar = namedtuple('ElectricCar', Car._fields + ('charge',))
```

### "Edit" a namedtuple

- shallow copies and replaces some fields

```python
my_car._replace(color='blue')
Car(color='blue', mileage=3812.4)
```

### Created a namedtuple from an iterable
```python
Car._make(['red', 999])
Car(color='red', mileage=999)
```

### When to use namedtuples

- only if it makes the code cleaner
- alternatives
   - dataclass (if you don't want immutability)
   - dict or list


## `NamedTuple`

Python 3.6+

```python
from typing import NamedTuple
class Car(NamedTuple):
    color: str
    mileage: float
    automatic: bool
    
car1 = Car('red', 3812.4, True)
>>> car1.mileage
3812.4
# Fields are immutable:
>>> car1.mileage = 12
AttributeError: "can't set attribute"
>>> car1.windshield = 'broken'
AttributeError:
"'Car' object has no attribute 'windshield'"
# Type annotations are not enforced without
# a separate type checking tool like mypy:
>>> Car('red', 'NOT_A_FLOAT', 99)
Car(color='red', mileage='NOT_A_FLOAT', automatic=99)
```

## [read-only attribute](https://www.pythonmorsels.com/making-read-only-attribute)

- use a `@property`

```python
class Square:
    def __init__(self, length):
        self._length = length
    @property
    def length(self):
        return self._length
```