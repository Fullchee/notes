## Setup

### Add `heroku` git remote

```bash
heroku git:remote -a app_name
```

## Connect to the file system

-   read-only access to your repo on the Heroku container

```bash
heroku run bash
```

## Connect to DB

```bash
heroku pg:psql --app app-name
```

### Connect to DB via Heroku VM

```bash
heroku run 'psql $DATABASE_URL' --app app-name
```

```bash
pg_dump -d `heroku config:get DATABASE_URL -a forma-1130-staging`t --no-owner --no-acl -Fc -f f.dump
```
