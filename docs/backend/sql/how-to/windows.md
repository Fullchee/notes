# Window functions

## [ROLLUP](https://www.postgresqltutorial.com/postgresql-rollup/)

- shorthand for defining multiple grouping sets
- really great for calculating groups for sums

![0dcda3d67b602afda521c9422556ba65.png](0dcda3d67b602afda521c9422556ba65.png)

```sql
SELECT
    brand,
    SUM (quantity)
FROM sales
GROUP BY ROLLUP (brand)
ORDER BY brand;
```

![b8d0bfbaa7a1960bac01fa38cf0c7182.png](b8d0bfbaa7a1960bac01fa38cf0c7182.png)

```sql
SELECT
    brand,
    segment,
    SUM (quantity)
FROM sales
GROUP BY ROLLUP (brand, segment)
ORDER BY brand, segment;
```

![dd4ba80a68ccfa70205a90823a83bdab.png](./dd4ba80a68ccfa70205a90823a83bdab.png)

## Window Functions

See SELECT STAR Julia Evans zine page 14

- `[expression] OVER ([window definition])`
- Window is a set of rows

- The window here is just one row

```sql
SELECT item,
  day - LAG(day) OVER (ORDER BY DAY)
FROM sales
```

- the window here is each class

```sql
SELECT ROW_NUMBER() OVER(
    PARTITION BY class
    ORDER BY grade DESC
  ) AS rank_in_class
```
