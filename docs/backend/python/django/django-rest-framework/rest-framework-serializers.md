# [DRF Serializers](https://www.django-rest-framework.org/api-guide/serializers/)

Nested model

```python
Dashboard
    name
    pages
```

```python
Pages
    name
    widgets
```

```python
Widgets
    name
```

## Deserializing (usage)

Database to JSON

```python
dashboards = DashboardSerializer(
    Dashboard.objects.all(), 
    many=True)
.data
```

## [SerializerMethodField](https://www.django-rest-framework.org/api-guide/fields/#serializermethodfield)

- return anything you want in the serializer data
- read-only
    - use a [`CustomField`](https://www.django-rest-framework.org/api-guide/fields/#custom-fields) if you want read/write

```python
class DashboardSerializer(serializers.ModelSerializer):
    dashboard_pages = serializers.SerializerMethodField("get_dashboard_pages")
    # just want an array of pages?
    # dashboard_pages = PageSerializer(many=True)

    class Meta:
        model = Page
        fields = ("id", "name", "dashboard_pages")

    def get_dashboard_pages(self, dashboard: Dashboard):
        page_query_set = Page.objects.filter(dashboard=dashboard)
        pages = PageSerializer(page_query_set, many=True, read_only=True).data
        return {page["id"]: page for page in pages}
```

## [Saving instances](https://www.django-rest-framework.org/api-guide/serializers/#saving-instances)

### Code in `view.py`

```python
try:
    dashboard = Dashboard.objects.get(id=id)
except Dashboard.DoesNotExist:
    pass

# updates if you pass an instance of the model
# DashboardSerializer(data=data) to create
serialized_dashboard = DashboardSerializer(dashboard, data=data)
if serialized_dashboard.is_valid(raise_exception=True):
    serialized_dashboard.save()  # triggers serializer update() or create()
```

### `update()`

```python
def update(self, instance: Dashboard, validated_data: dict):
    instance.name = validated_data.get("name", instance.name)
    instance.save()
    
    for page_data in pages:
        page = Page.objects.get(id=page_data["id"])
        serialized_page = PageSerializer(page, data=page_data)
        if serialized_page.is_valid(raise_exception=True):
            serialized_page.save()
```

### What is `validated_data`

When you pass in some data 

```python
DashboardSerializer(dashboard, data=data)
```

Django Rest Framework by default strips all of the properties that are
- read-only
- not listed in the `fields` of the serializer


#### Update a `1 to 1` foreign key

```
DashboardWidget <-> DashboardQuery
```

`DashboardWidget.query_file_path`

- string foreign key to `DashboardQuery`

- need to set the model

```python
instance.query = DashboardQuery.objects.get(file_path=file_path)
```

because we can't do `.update()` because we're given the instance and not a query set


## [Custom fields](https://www.django-rest-framework.org/api-guide/fields/#a-basic-custom-field)

```python
class ColorField(serializers.Field):
    """
    Color objects are serialized into 'rgb(#, #, #)' notation.
    """
    def to_representation(self, value):
        return "rgb(%d, %d, %d)" % (value.red, value.green, value.blue)

    def to_internal_value(self, data):
        data = data.strip('rgb(').rstrip(')')
        red, green, blue = [int(col) for col in data.split(',')]
        return Color(red, green, blue)
```

https://github.com/beda-software/drf-writable-nested
