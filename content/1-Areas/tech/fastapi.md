---
title: fastapi
draft: false
tags:
  - python
  - fastapi
  - backend
date: 2025-08-19
---
# [fastapi](https://fastapi.tiangolo.com/)

- a minimalist and fast backend framework based on [[starlette]] and [[pydantic]]
- should be used to build highly performant apis for production use

### creating an api

1. install fastapi

```
pip install fastapi
```

2. create a simple hello world api
```
from fastapi import FastAPI
app = FastAPI()

# GET request  
@app.get("/")
def index():
return {"message": "Hello, World!!"}
```

3. run the app on local
```
fastapi run dev
```


~aniket
## Links:

[[python]]
[[fastapi vs django vs flask]]

202508202229