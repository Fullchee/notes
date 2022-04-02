# Connecting to PSQL

## Connection string

`postgres://YourUserName:YourPassword@YourHostname:5432/YourDatabaseName`

## pg_dump

```bash
pg_dump -d postgres://postgres_connection_string --no-owner --no-acl -Fc -f dump_name.dump
```

- `-Fc` custom format (aka zipped)
- `-f` file name
- `-T` excludes a table, there can be multiple
- `-t` only include this table, there can be multiple

### pg_restore

````bash
pg_restore -d postgres://postgres_connection_string --no-owner --no-acl dump_name.dump
```-

* `-d` also accepts a local db name
* `--no-owner` removes the ownership
* `--no-acl` removes access privileges (grant/revoke commands)


#### Copy a table in the same db
```sql
CREATE TABLE new_table AS TABLE existing_table;
````

## Copy table to another database

```bash
pg_dump --no-owner --no-acl -t table_to_copy source_db | psql target_db
```

- dumps as a `.sql` file so you can just run with `psql`

## Cloud access

### Heroku

#### Connect to Heroku DB

```bash
heroku pg:psql --app app-name
```

#### Connect to your DB if you use Heroku but not their DB

```bash
heroku run 'psql $DATABASE_URL' --app app-name
```

### AWS RDS on a VPC via SSM

1. Create an ssh tunnel from your machine to an EC2 container in the VPC

```bash
aws ssm start-session --target "container-id-ec2, like i-0373fb85e5fbc7d8e" --document-name AWS-StartPortForwardingSession --parameters '{"portNumber":["22"],"localPortNumber":["56789"]}'
```

2. Connect to the
   - `ssh -p 56789 root@localhost`

- note the user should be `root` or whatever is expected on the EC2 machine
- not your personal username

3. `ssh root@127.0.0.1 -p 56789 -N -L 5433:{prod db url}:5432`
