### Context Manager

https://realpython.com/python-with-statement/#creating-function-based-context-managers

Create a function that can be used `with`
```python
    >>> @contextmanager
    ... def hello_context_manager():
    ...     print("Entering the context...")
    ...     yield "Hello, World!"
    ...     print("Leaving the context...")
    ...
    
    >>> with hello_context_manager() as hello:
    ...     print(hello)
    Entering the context...
    Hello, World!
    Leaving the context...
```