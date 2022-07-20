-   Testing: check out `pytest` and see why some people like it more than `unittest`

## Testing

### mock.patch

-   `patch` WHERE IT'S USED, not where it's defined
    -   the file only knows about what files are exported
    -   https://youtu.be/ww1UsGZV8fQ?t=434
-   3 ways of patching
    -   https://www.youtube.com/watch?v=WFRljVPHrkE

```py
@patch("path.where.my_function", autospec=True, spec_set=True)
class TestStuff(ApiTestCase):
    def test_stuff(self, mock_my_function):
```

#### [Patch Arguments](https://youtu.be/ww1UsGZV8fQ?t=1164)

-   `spec`: doesn't know about attributes of attributes
    -   should always at least `spec`
-   `autospec` doesn't know about dynamically created attributes
    -   example: class attributes
    -   work around: set the attribute that exists
    -   can be dangerous because it can trigger code on introspection
    -   can slow down tests
-   `spec_set=True` prevent setting properties that don't exist
-   `new_callable=MagicMock`is the default
    -   `new_callable=PropertyMock`
-   kwargs
    -   `return_value="lisa"
    -   `name="lisa"`
-   `patch.object`
-   `patch.dict`
-   `patch.multiple`

-   https://youtu.be/ww1UsGZV8fQ?t=889

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

-   You need `mock_check_output` because the decorator adds it
    -   what does it do???????????

patch for as little as possible, especially for

or use setUp() and tearDown()

## Expecting an Exception

```python
self.assertRaises(ExceptionType, func, arg1, arg2)
```

```python
self.assertRaises(ExceptionType, lambda: func(kwarg1="a", kwarg2="b"))
```