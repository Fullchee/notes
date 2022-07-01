## Why Pandas

Data structures for data analysis

-   series
-   data frames
-   stack

### Numpy vs Pandas

-   pandas is built in numpy arrays

https://pandas.pydata.org/docs/user_guide/10min.html

## Viewing data

https://pandas.pydata.org/docs/user_guide/10min.html#viewing-data

```python
# series
df.column_name
```

Operations & values on a column

```python
df.games_played.max()
df.points.mean()
```

## [Selection](https://pandas.pydata.org/docs/user_guide/10min.html#selection)

### [Get a single column](https://pandas.pydata.org/docs/user_guide/10min.html#getting)

```python
df.column_name
df["column_name"]
```

### Get rows

```python
df[0:3]
df["key1":"key2"]
```

.at, .iat

.loc

.iloc

```python
highest_price_index = df['price'].idxmax()
```

```python
print(df.iloc[highest_price_index].landmark)
```
