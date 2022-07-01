`left < right` or `left <= right`

-   `<=` because you gotta check that last value

How to calculate mid index?

-   `(left + right) // 2` could overflow if the indexes are huge
-   `left` + half the distance between left and right
    -   `left + (right - left) // 2`

```python
def binary_search(arr, target):
    left = 0
    right = len(arr) - 1

    while (left <= right):
        mid = left + (right - left) // 2
        if arr[mid] == target:
            return mid
        if arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
```
