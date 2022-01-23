## Dumping and Restoring

### Connection string
`postgres://YourUserName:YourPassword@YourHostname:5432/YourDatabaseName`

#### Get the Heroku DB connection string

```bash
pg_dump -d `heroku config:get DATABASE_URL --app app-name` --no-owner --no-acl -Fc -f dump_name.dump
```

### Download/Dump

```bash
pg_dump -d postgres://postgres_connection_string --no-owner --no-acl -Fc -f dump_name.dump
```

* `-Fc` custom format (aka zipped)
* `-f` file name
* `-T` excludes a table, there can be multiple
* `-t` only include this table, there can be multiple

### pg_restore
```bash
pg_restore -d postgres://postgres_connection_string --no-owner --no-acl dump_name.dump
```

* `-d` also accepts a local db name
* `--no-owner` removes the ownership
* `--no-acl` removes access privileges (grant/revoke commands)


#### Copy table to another database
```bash
pg_dump --no-owner --no-acl -t table_to_copy source_db | psql target_db
```
* dumps as a `.sql` file so you can just run with `psql`

## Access Commands

### Heroku 
#### Connect to your DB if you use Heroku but not their DB

```bash
heroku run 'psql $DATABASE_URL' --app app-name
```

#### Connect to Heroku DB

```bash
heroku pg:psql --app app-name
```

### AWS SSM

```bash
aws ssm start-session --target "container-id-ec2, like i-0373fb85e5fbc7d8e" --document-name AWS-StartPortForwardingSession --parameters '{"portNumber":["22"],"localPortNumber":["56789"]}'
```
* let's you ssh into the EC2 machine via your localhost 56789
* `ssh -p 56789 root@localhost`
    * note the user should be `root` or whatever is expected on the EC2 machine
    * not your personal username
#### Connect to that EC2 Instance


`ssh root@127.0.0.1 -p 56789 -N -L 5433:{prod db url}:5432`


## Debugging

### List all tables

* `\dt` for the current schema
* `\dt schema_name.*`

### List all column names
`\d+ <table_name>`

```sql
SELECT *
FROM information_schema.columns
WHERE table_schema = 'your_schema'
AND table_name   = 'your_table';
```

### Be able to view one row (if you have a ton of columns)

https://stackoverflow.com/questions/9604723/alternate-output-format-for-psql/16108898#16108898

![a580e45029c87021a93cc86cc9eba2bc.png](a580e45029c87021a93cc86cc9eba2bc.png)


#### `psqlrc`
In the files below, add this line
`\x auto`

* Mac
    * `~/.psqlrc`
* Windows
    * `%APPDATA\postgres`
    * https://stackoverflow.com/questions/64734341/where-is-the-psqlrc-file-on-windows





