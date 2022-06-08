# PSQL Shell

## Renaming

### Renaming a table

```sql
ALTER TABLE table_name
RENAME TO new_table_name;
```

### [Renaming a column](https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-rename-column/)

```sql
ALTER TABLE table_name 
RENAME COLUMN column_name TO new_column_name;
```

[PSQL Cheat Sheet](https://gist.github.com/Kartones/dd3ff5ec5ea238d4c546)

## Investigating

### List all tables

- `\dt` for the current schema
- `\dt schema_name.*`
- `\dt *.table_name`
  - to find all tables with that name

### List all column names

`\d+ <table_name>`

```sql
SELECT *
FROM information_schema.columns
WHERE table_schema = 'your_schema'
AND table_name   = 'your_table';
```

## Debugging PSQL

### Long running queries

```sql
SELECT pid, age(clock_timestamp(), query_start), usename, query
FROM pg_stat_activity
WHERE query != '<IDLE>' AND query NOT ILIKE '%pg_stat_activity%'
ORDER BY query_start desc;
```

### Blocked PIDs

```sql
select pid,
       usename,
       pg_blocking_pids(pid) as blocked_by,
       query as blocked_query
from pg_stat_activity
where cardinality(pg_blocking_pids(pid)) > 0;
```

## Recover your database after your computer suddenly turns off

- Make sure there's no `postgres` processes
  - `ps aux | ag postgres`
- `rm -f /usr/local/var/postgres/postmaster.pid`
- `brew services restart postgresql`
- `/usr/local/opt/postgres/bin/createuser -s postgres`
  - create the `postgres` user

### Create a CSV

```bash
psql -c "COPY (<select query>) TO STDOUT WITH CSV"
```

```bash
sudo -i -u postgres
```

* -i: launch shell with super user privileges
* -u: user