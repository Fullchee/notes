### Python Shell

```sh
python manage.py shell
```

```python
import django
django.setup()
from django.contrib.auth.models import User, Group
# other imports
```


## Tests

### Run a specific test
```shell
python manage.py test path.app.tests.ClassName --keepdb
```
?????

## Migrations

### Create an empty migration
```shell
python manage.py makemigrations api --name migration_example --empty
```


### Create a migration
operations list

- `migrations.RunPython(python_function_name),`
- `migrations.RunSQL("INSERT INTO product (title) VALUES ('Product1');"),`


## Querying

### SQL `where id in [1,3,4,5,6....];`

`.filter(id__in=[1, 3, 4, 5, 6....])`

