# Testing Django

## Factories

```python
import factory
from faker import Faker

from models import ModelName

faker = Faker()


class ModelName(factory.django.DjangoModelFactory):
    class Meta:
        model = ModelName

    name = factory.LazyAttributeSequence(lambda o, n: f"{faker.company()}_{n}.sql")

```

Factory uses faker

- https://faker.readthedocs.io/en/master/
