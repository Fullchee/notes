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
```python
python manage.py test path.app.tests.ClassName --keepdb
```

### 

## Querying

### SQL `where id in [1,3,4,5,6....];`

`.filter(id__in=[1, 3, 4, 5, 6....])`

