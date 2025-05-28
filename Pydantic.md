## Pydantic 
Pydantic is the most widely used data validation library for Python.

### Basic Example:

```

from datetime import datetime

from pydantic import BaseModel, PositiveInt


class User(BaseModel):
    id: int   # id is of type int; the annotation-only declaration tells Pydantic that this field is required. Strings, bytes, or floats will be coerced to integers if possible; otherwise an exception will be raised.
    name: str = 'John Doe'   # name is a string; because it has a default, it is not required.
    signup_ts: datetime | None  # signup_ts is a datetime field that is required, but the value None may be provided; Pydantic will process either a Unix timestamp integer (e.g. 1496498400) or a string representing the date and time.
    tastes: dict[str, PositiveInt]  #tastes is a dictionary with string keys and positive integer values. The PositiveInt type is shorthand for Annotated[int, annotated_types.Gt(0)].


external_data = {
    'id': 123,
    'signup_ts': '2019-06-01 12:22',  #The input here is an ISO 8601 formatted datetime, but Pydantic will convert it to a datetime object. 
    'tastes': {
        'wine': 9,
        b'cheese': 7, #The key here is bytes, but Pydantic will take care of coercing it to a string. 
        'cabbage': '1',  
    },
}

user = User(**external_data)  
print(user) # id=123 name='John Doe' signup_ts=datetime.datetime(2019, 6, 1, 12, 22) tastes={'wine': 9, 'cheese': 7, 'cabbage': 1}
print(user.id)   #123

print(user.model_dump())  
"""
{
    'id': 123,
    'name': 'John Doe',
    'signup_ts': datetime.datetime(2019, 6, 1, 12, 22),
    'tastes': {'wine': 9, 'cheese': 7, 'cabbage': 1},
}
"""
"""

```


### Pydantic v1 vs Pydantic v2
