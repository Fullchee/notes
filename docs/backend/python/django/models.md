# Django Models

https://betterprogramming.pub/everything-you-need-to-know-about-django-models-in-python-2a44ed4293dd

1. startproject and startapp

UUIDField as primary key

-   cluster index?
    -   don't use UUIDs

```python
  AGE_RATING =[
    ("G","General Audiences"),
    ("PG","Parental Guidance Suggested"),
    ("PG-13","Inappropriate for Children Under 13" ),
    ("R", "Restricted"),
    ("NC-17","Adults Only"),
  ]

age_rating = models.CharField(max_length= 5, choices = AGE_RATING, default = "GENERAL AUDIENCE")

```

Choices

Validators

Migrations

Django Admin

Customizing the Django Admin

`__str__` representation of

Metadata

-   unique constraints
-   ordering

Adding Django context
