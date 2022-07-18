# [Swagger (drf-yasg)](https://drf-yasg.readthedocs.io/en/stable/readme.html)


## `GET`

```python
from drf_yasg.utils import swagger_auto_schema
from drf_yasg import openapi

@swagger_auto_schema(
    method="get",
    manual_parameters=[
        Parameter("secret", openapi.IN_HEADER, type="string"),
        Parameter("query_param", openapi.IN_QUERY, type="string"),
    ],
    operation_description="",
)
```

## `POST`

```python
from drf_yasg.utils import swagger_auto_schema
from drf_yasg import openapi
@swagger_auto_schema(
    method="post",  # remove this for class based
    request_body=openapi.Schema(
        type=openapi.TYPE_OBJECT,
        required=["geo", "month", "year"],
        properties={
            "name": openapi.Schema(type=openapi.TYPE_STRING, description="example: "),
        },
    ),
    responses={202: ""},
)
@api_view(["POST"])
@permission_classes((IsSuperUser,))
def post_something(request):
    name = request.data["name"]
```