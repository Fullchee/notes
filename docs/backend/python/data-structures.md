# Data structures

## [Lists](https://fullchee.github.io/notes/backend/python/python-lists)

## [Dicts](https://fullchee.github.io/notes/backend/python/dict/)
## Stacks
- list
    - amortized O(1) for inserts and deletes

### `collections.deque`
- double-ended queue
    - linked list

Adding: stack is the same as queue
```python
>>> from collections import deque
>>> s = deque()
>>> s.append('eat')
```

```python
>>> s.pop()
'eat'
>>> s.pop()
IndexError: "pop from an empty deque"
```

### `queue.LifoQueue`
- multi-producers & multi-consumers from different threads
    - same process

```python
>>> from queue import LifoQueue
>>> s = LifoQueue()
>>> s.put('eat')
>>> s.get()
'eat'
>>> s.get_nowait()
queue.Empty
>>> s.get()
# Blocks / waits forever...
```


## Queues

### `collections.deque`

Adding: stack is the same as queue

```python
>>> from collections import deque
>>> q = deque()
>>> q.append('eat')
```

```python
>>> q.popleft()
'eat'
>>> q.popleft()
IndexError: "pop from an empty deque"
```


### `queue.Queue`

- multi-producers & multi-consumers from different threads
    - same process

```python
>>> from queue import Queue
>>> q = Queue()
>>> q.put('eat')
```

```python
>>> q.get()
'eat'
>>> q.get_nowait()
queue.Empty
>>> q.get()
# Blocks / waits forever...
```

### [`multiprocessing.Queue`](https://stackoverflow.com/a/30294648/8479344)

- similar to `queue.Queue`
- also handles different processes vs threads


## Priority Queue

### `heapq`

- binary heap

```python
from heapq import heapq

pq = []

heappush(pq.(2, 'code'))
```


### `queue.PriorityQueue`

- wrapper around `heapq`
- supports concurrency (locks, threads, ...)
- API is class based

```python
from queue import PriorityQueue

q = PriorityQueue()
q.put((2, 'code'))
q.put((1, 'eat'))
q.put((3, 'sleep'))
```

