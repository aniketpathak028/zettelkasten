---
title: fastapi
draft: false
tags:
  - python
  - fastapi
  - backend
date: 2025-08-19
description: fastapi and why it you should know it?
---
# [fastapi](https://fastapi.tiangolo.com/)

- a minimalist and fast backend framework based on [[starlette]] and [[pydantic]]
- should be used to build highly performant apis for production use

### creating an api

1. install fastapi

```python
pip install fastapi
```

2. create a simple hello world api
```python
from fastapi import FastAPI
app = FastAPI()

# GET request  
@app.get("/")
def index():
return {"message": "Hello, World!!"}
```

3. run the app on local
```python
fastapi run dev
```


## Links:

[[python]]
[[fastapi vs django vs flask]]

202508202229