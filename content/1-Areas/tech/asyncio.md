---
title: asyncio
draft: true
tags:
  - asyncio
  - python
  - async
date: 2025-08-19
---
# asyncio

Asynchronous programming allows our code to be more efficient by doing multiple things at once without any unnecessary waiting. Asyncio is your choice for running multiple tasks concurrently such as network requests or reading files, without using much CPU power.

The event-loop handles the asyncio tasks, which are defined using the `async def` syntax. You can use `await` to pause the execution of a coroutine until the awaited task is complete. The event loop runs the tasks in a non-blocking way, allowing other tasks to run while waiting for I/O operations to complete.

~aniket

## Links:

[[python]]
[[async]]

202508202231