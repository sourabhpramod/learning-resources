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
### Add the following to pyproject.toml file
```txt
[tool.pytest.ini_options]
pythonpath = "src"
```

### Docker Setup
Create a file "compose.yaml"
```
name: todo-app
services:
  nginx:
    image: nginx:1.17
    volumes:
      - ./nginx/nginx.conf:/etc/nginx/conf.d/default.conf
    ports:
      - 8000:80
    depends_on:
      - backend
      - frontend
  frontend:
    image: "node:22"
    user: "node"
    working_dir: /home/node/app
    environment:
      - NODE_ENV=development
      - WDS_SOCKET_PORT=0
    volumes:
      - ./frontend/:/home/node/app
    expose:
      - "3000"
    ports:
      - "3000:3000"
    command: "npm start"
  backend:
    image: todo-app/backend
    build: ./backend
    volumes:
      - ./backend/:/usr/src/app
    expose:
      - "3001"
    ports:
      - "8001:3001"
    command: "python src/server.py"
    environment:
      - DEBUG=true
    env_file:
      - path: ./.env
        required: true
```
## Ngnix config
Create a directory "nginx" in root
Create file "nginx.config"
inside nginx.config:
```txt

server {
    listen 80;
    server_name farm_intro;

    location / {
        proxy_pass http://frontend:3000;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
    }

    location /api {
        proxy_pass http://backend:3001/api;
    }
}

```


### File Creation:
Create a folder "src" inside backend (outside venv) and add two files : "dal.py", "server.py"

## To-Do List Code:
### dal.py:
```python

from bson import ObjectId
from motor.motor_asyncio import AsyncIOMotorCollection
from pymongo import ReturnDocument

from pydantic import BaseModel

from uuid import uuid4

class ListSummary(BaseModel):
  id: str
  name: str
  item_count: int

  @staticmethod
  def from_doc(doc) -> "ListSummary":
      return ListSummary(
          id=str(doc["_id"]),
          name=doc["name"],
          item_count=doc["item_count"],
      )

class ToDoListItem(BaseModel):
  id: str
  label: str
  checked: bool

  @staticmethod
  def from_doc(item) -> "ToDoListItem":
      return ToDoListItem(
          id=item["id"],
          label=item["label"],
          checked=item["checked"],
      )

class ToDoList(BaseModel):
  id: str
  name: str
  items: list[ToDoListItem]

  @staticmethod
  def from_doc(doc) -> "ToDoList":
      return ToDoList(
          id=str(doc["_id"]),
          name=doc["name"],
          items=[ToDoListItem.from_doc(item) for item in doc["items"]],
      )

class ToDoDAL:
  def __init__(self, todo_collection: AsyncIOMotorCollection):
      self._todo_collection = todo_collection

  async def list_todo_lists(self, session=None):
      async for doc in self._todo_collection.find(
          {},
          projection={
              "name": 1,
              "item_count": {"$size": "$items"},
          },
          sort={"name": 1},
          session=session,
      ):
          yield ListSummary.from_doc(doc)

  async def create_todo_list(self, name: str, session=None) -> str:
      response = await self._todo_collection.insert_one(
          {"name": name, "items": []},
          session=session,
      )
      return str(response.inserted_id)

  async def get_todo_list(self, id: str | ObjectId, session=None) -> ToDoList:
      doc = await self._todo_collection.find_one(
          {"_id": ObjectId(id)},
          session=session,
      )
      return ToDoList.from_doc(doc)

  async def delete_todo_list(self, id: str | ObjectId, session=None) -> bool:
      response = await self._todo_collection.delete_one(
          {"_id": ObjectId(id)},
          session=session,
      )
      return response.deleted_count == 1

  async def create_item(
      self,
      id: str | ObjectId,
      label: str,
      session=None,
  ) -> ToDoList | None:
      result = await self._todo_collection.find_one_and_update(
          {"_id": ObjectId(id)},
          {
              "$push": {
                  "items": {
                      "id": uuid4().hex,
                      "label": label,
                      "checked": False,
                  }
              }
          },
          session=session,
          return_document=ReturnDocument.AFTER,
      )
      if result:
          return ToDoList.from_doc(result)

  async def set_checked_state(
      self,
      doc_id: str | ObjectId,
      item_id: str,
      checked_state: bool,
      session=None,
  ) -> ToDoList | None:
      result = await self._todo_collection.find_one_and_update(
          {"_id": ObjectId(doc_id), "items.id": item_id},
          {"$set": {"items.$.checked": checked_state}},
          session=session,
          return_document=ReturnDocument.AFTER,
      )
      if result:
          return ToDoList.from_doc(result)

  async def delete_item(
      self,
      doc_id: str | ObjectId,
      item_id: str,
      session=None,
  ) -> ToDoList | None:
      result = await self._todo_collection.find_one_and_update(
          {"_id": ObjectId(doc_id)},
          {"$pull": {"items": {"id": item_id}}},
          session=session,
          return_document=ReturnDocument.AFTER,
      )
      if result:
          return ToDoList.from_doc(result)
```
### server.py
```python
from contextlib import asynccontextmanager
from datetime import datetime
import os
import sys

from bson import ObjectId
from fastapi import FastAPI, status
from motor.motor_asyncio import AsyncIOMotorClient
from pydantic import BaseModel
import uvicorn

from dal import ToDoDAL, ListSummary, ToDoList

COLLECTION_NAME = "todo_lists"
MONGODB_URI = os.environ["MONGODB_URI"]
DEBUG = os.environ.get("DEBUG", "").strip().lower() in {"1", "true", "on", "yes"}


@asynccontextmanager
async def lifespan(app: FastAPI):
    # Startup:
    client = AsyncIOMotorClient(MONGODB_URI)
    database = client.get_default_database()

    # Ensure the database is available:
    pong = await database.command("ping")
    if int(pong["ok"]) != 1:
        raise Exception("Cluster connection is not okay!")

    todo_lists = database.get_collection(COLLECTION_NAME)
    app.todo_dal = ToDoDAL(todo_lists)

    # Yield back to FastAPI Application:
    yield

    # Shutdown:
    client.close()


app = FastAPI(lifespan=lifespan, debug=DEBUG)


@app.get("/api/lists")
async def get_all_lists() -> list[ListSummary]:
    return [i async for i in app.todo_dal.list_todo_lists()]


class NewList(BaseModel):
    name: str


class NewListResponse(BaseModel):
    id: str
    name: str


@app.post("/api/lists", status_code=status.HTTP_201_CREATED)
async def create_todo_list(new_list: NewList) -> NewListResponse:
    return NewListResponse(
        id=await app.todo_dal.create_todo_list(new_list.name),
        name=new_list.name,
    )


@app.get("/api/lists/{list_id}")
async def get_list(list_id: str) -> ToDoList:
    """Get a single to-do list"""
    return await app.todo_dal.get_todo_list(list_id)


@app.delete("/api/lists/{list_id}")
async def delete_list(list_id: str) -> bool:
    return await app.todo_dal.delete_todo_list(list_id)


class NewItem(BaseModel):
    label: str


class NewItemResponse(BaseModel):
    id: str
    label: str


@app.post(
    "/api/lists/{list_id}/items/",
    status_code=status.HTTP_201_CREATED,
)
async def create_item(list_id: str, new_item: NewItem) -> ToDoList:
    return await app.todo_dal.create_item(list_id, new_item.label)


@app.delete("/api/lists/{list_id}/items/{item_id}")
async def delete_item(list_id: str, item_id: str) -> ToDoList:
    return await app.todo_dal.delete_item(list_id, item_id)


class ToDoItemUpdate(BaseModel):
    item_id: str
    checked_state: bool


@app.patch("/api/lists/{list_id}/checked_state")
async def set_checked_state(list_id: str, update: ToDoItemUpdate) -> ToDoList:
    return await app.todo_dal.set_checked_state(
        list_id, update.item_id, update.checked_state
    )


class DummyResponse(BaseModel):
    id: str
    when: datetime


@app.get("/api/dummy")
async def get_dummy() -> DummyResponse:
    return DummyResponse(
        id=str(ObjectId()),
        when=datetime.now(),
    )


def main(argv=sys.argv[1:]):
    try:
        uvicorn.run("server:app", host="0.0.0.0", port=3001, reload=DEBUG)
    except KeyboardInterrupt:
        pass


if __name__ == "__main__":
    main()

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
