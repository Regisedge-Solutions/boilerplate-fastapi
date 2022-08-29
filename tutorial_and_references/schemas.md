# Schemas (Pydantic models)
* Used to specifying and validating inputs and outputs to the API. 
* Note that this is different from datamodels (models.py) which are used for interacting with the database.

```
pip install pydantic 
pip install pydantic[email]
pip install pydantic[dotenv]


from pydantic import BaseModel
from pydantic import ValidationError
```

### Pydantic Models (schemas)
Can specify different input and output models

```
class Item(BaseModel):
    name: str
    description: Union[str, None] = None # The description can be a str or None and the default value is None
    price: float
    tax: Union[float, None] = None
    tags: List[str] = [] # List of strings, with default as an empty string 


class UserIn(BaseModel):
    username: str
    password: str
    email: EmailStr
    full_name: Union[str, None] = None

class UserOut(BaseModel):
    username: str
    email: EmailStr
    full_name: Union[str, None] = None

```

### Usage of schemas

```
@app.post("/user/", response_model=UserOut)
async def create_user(user: UserIn):
    return user


# String validations of query parameters
Union[str, None] = Query(default=None, min_length=3, max_length=50)

Union[str, None] = Query(default=None)
has the same effect as  
Union[str, None] = None


try:
    User(signup_ts='broken', friends=[1, 2, 'not number'])
except ValidationError as e:
    print(e.json())

```

## References 
Pydantic 
https://pydantic-docs.helpmanual.io/
https://pydantic-docs.helpmanual.io/usage/models/

Usage in FastAPI
https://fastapi.tiangolo.com/tutorial/response-model/
