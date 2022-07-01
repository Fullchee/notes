# Boolean

Casting text to boolean

-   `t`, `true`, `y`, `yes`, `on`, `1`
-   `f`, `false`, `n`, `no`, `off`, `0`

```sql
select 'true'::boolean, 'false'::boolean;

 bool | bool
------+------
 t    | f
(1 row)
```

```sql
select 'a'::BOOLEAN;
ERROR:  invalid input syntax for type boolean: "a"
LINE 1: select 'a'::BOOLEAN;
```
