---
title: building ai agent to troubleshoot k8s cluster
draft: false
tags:
  - ai-agents
  - k8s
  - troubleshooting
  - devops
  - gemini
  - agent-development-kit
date: 2026-10-17
description: building, deploying, governing and scaling AI agents for k8s cluster
---
# building and deploying an AI agent to troubleshoot k8s cluster


### 1. prototype vs production

Day-1: The prototype

- we can simply create a k8s-agent by using a coding agent and connecting it with a k8s mcp server and it can help us on day-1 with simple troubleshooting tasks but the real problem arises when we try to deploy this agent into production

![[Pasted image 20261017131028.png]]

Challenges:

![[Pasted image 20261017131238.png|477]]

we can simply create an agent using langchain, langgraph, MCP etc but is it safe to deploy it into production? No because prototype != production
- trust -> can we really trust it in production? We are going to use a feature called **Agent Evaluation** to tackle this!
- runtime -> what if we need to scale the agent to multiple users, handle multiple incidents and restart the agent when it crashes? We will be using **Agent Runtime** to tackle this!
- memory -> how can the agent remember the previous issues? we use **Memory Bank**
- identity -> how do we handle the access rights of the agent? **Agent Identity + SPIFFY**
- observability and cost -> how to track the actions of the agent? **Google cloud cost + Model garden feat**

### 2. Building the agent using Gemini Agent Development Kit

We are going to build an AI agent to troubleshoot a k8s cluster which is a very tedious process for a devops engineer so that this process can be automated easily and we are going to build it using Gemini ADK! Why?

- we want to have a complex agent that can have context management, session management, model selection, MCP integration etc
- writing all of this will take a lot of time so we can use Gemini ADK and build this agent using simple natural language prompts using Agent CLI without writing any code!
- Agent CLI has a bunch of skills that can help build several features for our Agent 

![[Pasted image 20261017134651.png]]




## Links:

202610171137
