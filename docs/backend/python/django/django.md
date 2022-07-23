## Reading list

-   [How to Use Materialized View in Django](https://medium.com/analytics-vidhya/how-to-use-materialized-view-in-django-3b91f71f718a)
-   [Asynchronous Tasks With Django and Celery](https://realpython.com/asynchronous-tasks-with-django-and-celery)

[Write your own commands](https://docs.djangoproject.com/en/dev/howto/custom-management-commands/)

-   `app_name/management/commands`

## Django (`manage.py`) scripts

### Creating your custom commands

1. Create a file called: `app_name/management/commands/create_admin_superuser.py`
2. Fill in the blanks


#### When would you want to write your own command?

```python
from django.core.management.base import BaseCommand

class Command(BaseCommand):
    help = """ help string """

    def add_arguments(self, parser):
        parser.add_argument("email", type=str)
        parser.add_argument("password", type=str)

    def handle(self, *args, **options):
        # do stuff
        self.stdout.write("Created an admin superuser")
```

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

`manage.py shell` vs `python` console

-   `manage.py shell` sets the `DJANGO_SETTINGS_MODULE`which lets it know about the `settings.py`

(`django_extensions` has a `shell_plus`)

### [`django_extensions`](https://github.com/django-extensions/django-extensions)

[video](https://vimeo.com/1720508?embedded=true&source=vimeo_logo&owner=627770)

adds a bunch of nice helpers to `./manage.py`

-   `graph_models`
    -   graphs your models
-   `runserver_plus`
    -   django error page with a Python terminal to see the info
-   `runscript`
    -   run a python file that sets up django (import django, django.setup())
    -   nice for scripts that are run with cron
-   `shell_plus`
    -   django shell that loads all of your models
-   `print_user_for_session <session_ID>`
    -   get all of the session info for a user

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

### Override settings

```python
from django.test import override_settings

class TestBuildPath(TestCase):
    @override_settings(CLIENT_ID=1130)
    def test_overriding_settings(self):
        self.assertEqual(settings.CLIENT_ID, 1130)
```

### Expect raising an error

```python
self.assertRaises(ExpectedException, fn_name, arg1, arg2)
```

### Testing endpoints

If you really need to test the endpoint instead of a function

https://www.django-rest-framework.org/api-guide/testing/

```python
from rest_framework.test import APIRequestFactory, force_authenticate

def create_request(endpoint: str, user: User, query_params: Dict = None):
    factory = APIRequestFactory()
    request = factory.get(endpoint)
    request.user = user
    force_authenticate(request, user=user)
    request.GET = query_params or {}
    return request

user = User.objects.create_user(
        username="username",
        email="username@username.com",
        password="password",
    )

request = create_request(f"app_name/endpoint_name", user, query_params)
response = view_fn(request)
```

## Models

### [`null=True` vs `blank=True`](https://stackoverflow.com/questions/8609192/what-is-the-difference-between-null-true-and-blank-true-in-django)

-   `blank=True` can leave it blank for forms
    -   example: Django admin form
-   `null=True` the value in the table can be `NULL`

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

-   https://realpython.com/create-django-index-without-downtime/#non-atomic-migrations

## Querying

### SQL `where id in [1,3,4,5,6....];`

```python
.filter(id__in=[1, 3, 4, 5, 6....])
```


```python
model_name.filter().values()
```

### [.filter(id=1, name=1) and .filter(id=1).filter(name=1)](https://stackoverflow.com/a/21364751/8479344)

- they only might be different when dealing with foreign keys


### Set a foreign key to be something other than an ID

```python
class DashboardWidget(models.Model):
    query = models.ForeignKey(
        DashboardQuery,  # the foreign model
        to_field="file_path",  # DashboardQuery.file_path, must be unique
        db_column="query_file_path",  # name of the db column, default: query_id (field-name_id)
        ...
    )
```

Doing a migration?
- you need to drop the `DashboardWidget.query` and then re-create it
- `AlterField` doesn't change the column type from `int` to `text` in Django 2.2


