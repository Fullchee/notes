## Data Structures

### Queue

```python
collections.dequeue # double ended queue
```

#### Unshift the first item in an array

```python
first_value = arr.pop(0)  # O(n)


```

### defaultdict

```python
my_dict = collections.defaultdict(int)  # default value: 0
my_dict[key] += 1
```

### Counter: TODO

```python
collections.counter
```

```python
class Solution:
    def fourSumCount(self, A: List[int], B: List[int], C: List[int], D: List[int]) -> int:
        m = collections.defaultdict(int)
        lists = [A, B, C, D]

        def nSumCount() -> int:
            addToHash(0, 0)
            return countComplements(len(lists) // 2, 0)

        def addToHash(i: int, total: int) -> None:
            if i == len(lists) // 2:
                m[total] += 1
            else:
                for a in lists[i]:
                    addToHash(i + 1, total + a)

        def countComplements(i: int, complement: int) -> int:
            if i == len(lists):
                return m[complement]
            cnt = 0
            for a in lists[i]:
                cnt += countComplements(i + 1, complement - a)
            return cnt

        return nSumCount()
```
