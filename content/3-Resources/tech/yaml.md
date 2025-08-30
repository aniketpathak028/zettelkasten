---
title: yaml
draft: false
tags:
  - yaml
  - data-serialization
  - devops
date: 2025-08-25
description: yaml is easy
---
# yaml

- human readable
- data-serialization
- language

alternative: json

advantages of yaml over json:
- yaml is better suited for devops ppl
- can add comments in yaml
- yaml is easier to read

usecase:
- k8s
- docker compose
- ansible
- cicd

```yaml
# key value pairs
key: value

# yaml object
key:
  key1: value1
  key2: value2
  key3: value3

# list
tools: 
  - k8s
  - docker
  - ansible
	  
# nested dict and list
server:
  name: demo-server
  ports:
    - 80
    - 8080
    - 3036
```








## Links:

202508250040