## Reading list
* [How to Use Materialized View in Django](https://medium.com/analytics-vidhya/how-to-use-materialized-view-in-django-3b91f71f718a)
* [Asynchronous Tasks With Django and Celery](https://realpython.com/asynchronous-tasks-with-django-and-celery)


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
python manage.py test path.app.tests.ClassName.testName --keepdb
```

### Create fake data from a factory
```py
from app.path_name import MyModel
MyModel.create_batch(200)
```

## Models

### [`null=True` vs `blank=True`](https://stackoverflow.com/questions/8609192/what-is-the-difference-between-null-true-and-blank-true-in-django)

* blank: is the field required for forms?

## Migrations

### Create an empty migration

useful when you're creating a custom migration
```shell
python manage.py makemigrations app_name --name migration_name --empty
```


### Create a migration
operations list

```python
migrations.RunPython(python_function_name),
migrations.RunSQL("INSERT INTO product (title) VALUES ('Product1');"),
```

#### Reverse a migration
```python
operations = [
        migrations.RunSQL(
            'CREATE INDEX "app_sale_sold_at_b9438ae4" '
            'ON "app_sale" ("sold_at");',

            reverse_sql='DROP INDEX "app_sale_sold_at_b9438ae4";',
        ),
    ]
```

Then `python manage.py migrate app_name 0008

#### Add an index to a table that already has a ton of data in it
* https://realpython.com/create-django-index-without-downtime/#non-atomic-migrations


## Querying

### SQL `where id in [1,3,4,5,6....];`

```python
.filter(id__in=[1, 3, 4, 5, 6....])
```

### Pretty print

```python
model_name.filter().values()
```
* doesn't work on the actual instance
* ?????