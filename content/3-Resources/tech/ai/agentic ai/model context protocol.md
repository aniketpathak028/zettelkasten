---
title: model context protocol
draft: false
tags:
  - mcp
  - ai
date: 2026-09-08
description: what is model context protocol?
---
# model context protocol

mcp - https://modelcontextprotocol.io/introduction

- a communication layer that provides AI with context and tools without requiring us to write a bunch of tedious integration code!
- mcp - transport agnostic communication meaning can communicate in standard IO, http, websockets, various other networks protocols

![[Pasted image 20260908233812.png]]

- we can use the official python sdk mcp to write mcp servers easily
- the sdk uses decorators to define tools so instead of writing JSON schemas manually, we can use python type hints and field descriptions.
- the sdk automatically generates the schema that claude understands

## Key Benefits of the SDK Approach

- No manual JSON schema writing required
- Type hints provide automatic validation
- Clear parameter descriptions help Claude understand tool usage
- Error handling integrates naturally with Python exceptions
- Tool registration happens automatically through decorators

## Links:

202609082302
