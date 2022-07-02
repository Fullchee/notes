# Square bracket notation

## Dict

When you need to get a value in a dict, you pass in the key (the 'word' using the dictionary analogy)

Then Python will fetch what the corresponding value is.

```py
my_dict = {'a': 'alpha', 'b': 'beta'}
my_dict['a']  # 'alpha'
```

## Lists

You can think of lists like special dictionaries.

The OG dictionary 😎

That's why they both use square brackets (my guess ¯\\_(ツ)_/¯)

```py
my_list = ['a', 'b', 'c']

my_list[0]  # 'a'
```

is similar to this dictionary

```py
my_listy_dict = {
  0: 'a',
  1: 'b',
  2: 'c',
}

my_listy_dict[0]  # 'a'
```

## Double square brackets

A list can't be a key for a dictionary (I'll explain that later)

if you could though, then it would look like this

```py
# my_key = ['price', 'size_in_sqft']

# my_weird_dict[my_key]
```

Which is the same as

```py
my_weird_dict[['price', 'size_in_sqft']]
```
