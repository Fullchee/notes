### Filter by date within the current fiscal year (starts Feb 1)

```sql
SELECT *
FROM table
WHERE DATE_PART('year', date_column_name - '1 month'::INTERVAL) =
      DATE_PART('year', CURRENT_DATE::date - '1 month'::INTERVAL)
```

### How UNNEST works

```sql
SELECT
UNNEST(ARRAY\[1,2,3\]) as num1
UNNEST(ARRAY\[[[javascript]] javascript.md4,5\]) as num2
1 as one
```

![4f091a049cccf838fa97c4f8ead2ce88.png](4f091a049cccf838fa97c4f8ead2ce88.png)

### Using UNNEST

```sql
SELECT
    UNNEST(ARRAY[quota1_building_block_id, quota2_building_block_id]) AS rule_block_id,
    *
    FROM commissions_internal_formatts
WHERE payee_id = 483674
```
![0d2b09974a338b8855490ef96c2d6960.png](0d2b09974a338b8855490ef96c2d6960.png)
