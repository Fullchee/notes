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