## Steps to use and develop with FastAPI

First step:
```bash
pip install "fastapi[standard]"
```
Create a new file named main.py

```python
#define all routes and whatever needed here and run the server

from typing import Union
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"Hello": "World"} #json response

@app.get("/items/{item_id}")
def read_item(item_id: int, q: Union[str, None]=None):
    return {"item_id": item_id, "q": q}

```
To run server:
```bash
pip install uvicorn
```
```bash
uvicorn main:app --reload
```

For structured input requests (instead of standard json):
```python
from pydantic import BaseModel
app = FastAPI()

class Item(BaseModel):
    name: str
    price: float
    is_offer: Union[bool, None]= None

@app.put("/items/{item_id}")  #for modification
def update_item(item_id: int, item: Item):
    return {"item_name": item.name, "item_id": item_id}

```
