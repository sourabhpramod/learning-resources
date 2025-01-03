## Virtual Env setup and basic set up in backend directory:
to create:
```bash
python -m venv venv
```
to activate:
```bash
.\venv\Scripts\Activate
```
### Creating the files necessary in backend dir:
Create file "Dockerfile" 
Create file "pyproject.toml"

### Project set up:
First installation
```bash
pip install "fastapi[all]" motor[srv] beanie aiostream
```
generate requirements.txt file:
```bash
pip freeze > requirements.txt
```
### Add the following to Dockerfile

```txt
FROM python:3

WORKDIR /usr/src/app
COPY requirements.txt ./

RUN pip install --no-cache-dir --upgrade -r ./requirements.txt

EXPOSE 3001

CMD ["python", "./src/server.py"]
```

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
