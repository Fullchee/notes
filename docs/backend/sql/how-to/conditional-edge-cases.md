# Conditionals and edge cases

## CASE

```sql
CASE (value)
  WHEN "one" THEN 1
  WHEN "two" THEN 2
  ELSE 0
END;

CASE
  WHEN conditional = :conditional THEN 1
  ELSE 0
END;
```

### Add a fallback row if there are no rows in the initial value

```sql
SELECT c1, ...

UNION

SELECT 0 AS c1
LIMIT 1;
```

## UNNEST arrays

see json and arrays page

useful where you want to get bt1 and bt2 arrays and match those values at the same time
