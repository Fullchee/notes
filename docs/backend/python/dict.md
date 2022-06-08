# Python Dictionaries

### Get the key with the max value in the dict
```python
stats = {'a': 1, 'b': 3000, 'c': 0}
max(stats, key=stats.get)  # 'b'

max(stats, key=lambda key: stats[key])  # 'b'
```

### [ChainMap](https://florimond.dev/en/posts/2018/07/a-practical-usage-of-chainmap-in-python/#example-the-shopping-inventory)

#### Maintaining a precedence chain of defaults

```python
cli_args = {"debug": True}
defaults = {"debug": False}

config = ChainMap(cli_args, defaults)
config["debug"]  # True

# looks for the key in cli_args and then in defaults
```

### [UserDict](https://realpython.com/python-collections-module/#customizing-built-ins-userstring-userlist-and-userdict)

When you want to modify the behaviour of the built-in dict