Python Tricks Chapter 2.4

## `_var`
* convention: "pseudo" private
* you shouldn't use this private function, var, ...

## `var_`

* convention: avoid naming conflicts with built-in Python keywords

```python
def make_object(name, class_, type_):
    ...
```

## `__var`

* name mangling
* really makes it annoying to use that variable outside of the class

```python
class Test:
    def __init__(self):
        self.__ghost = "Casper"
        
    def get_ghost(self):
        return self.__ghost  # this works!
    
    def __fn_ghost(self):
        ...

t = Test()
t.__ghost  # AttributeError!
t._Test__ghost  # "Casper", name mangles!
```


```python
class SuperTest(Test):
    def __init__(self):
        super().__init__()  # no name mangling!
        self.__ghost = "overridden"

st = SuperTest()
st.__ghost  # AttributeError
st._SuperTest__ghost  # "overridden"
st._Test__ghost  # "Casper"
```


## `__var__`

* not name mangled
* convention: reserved for built-in magic methods


## `_` as a var name

* convention: name for a var that you won't use

```python
for _ in range(32):
    print('Hi')
```

```python
car = ('red', 'auto', 12, 3812.4)
color, _, _, mileage = car
```

* Python REPL: the value of the previous expression

```python
>>> 20 + 3
23
>>> _
23
```

```python
>>> list()
[]
>>> _.append(1)
>>> _.append(2)
>>> _.append(3)
```