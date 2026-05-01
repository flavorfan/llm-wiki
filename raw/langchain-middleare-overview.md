---
title: "Overview"
source: "https://docs.langchain.com/oss/python/langchain/middleware/overview"
author:
published:
created: 2026-04-21
description: "Control and customize agent execution at every step"
tags:
  - "clippings"
---
Middleware provides a way to more tightly control what happens inside the agent. Middleware is useful for the following:
- Tracking agent behavior with logging, analytics, and debugging.
- Transforming prompts, [tool selection](https://docs.langchain.com/oss/python/langchain/middleware/built-in#llm-tool-selector), and output formatting.
- Adding [retries](https://docs.langchain.com/oss/python/langchain/middleware/built-in#tool-retry), [fallbacks](https://docs.langchain.com/oss/python/langchain/middleware/built-in#model-fallback), and early termination logic.
- Applying [rate limits](https://docs.langchain.com/oss/python/langchain/middleware/built-in#model-call-limit), guardrails, and [PII detection](https://docs.langchain.com/oss/python/langchain/middleware/built-in#pii-detection).
Add middleware by passing them to [`create_agent`](https://reference.langchain.com/python/langchain/agents/factory/create_agent):

```python
from langchain.agents import create_agent
from langchain.agents.middleware import SummarizationMiddleware, HumanInTheLoopMiddleware

agent = create_agent(
    model="gpt-5.4",
    tools=[...],
    middleware=[
        SummarizationMiddleware(...),
        HumanInTheLoopMiddleware(...)
    ],
)
```

## The agent loop

The core agent loop involves calling a model, letting it choose tools to execute, and then finishing when it calls no more tools:![Core agent loop diagram](https://mintcdn.com/langchain-5e9cc07a/Tazq8zGc0yYUYrDl/oss/images/core_agent_loop.png?w=2500&fit=max&auto=format&n=Tazq8zGc0yYUYrDl&q=85&s=41eb4f053ed5e6b0ba5bad2badf6d755)

Core agent loop diagram

Middleware exposes hooks before and after each of those steps:![Middleware flow diagram](https://mintcdn.com/langchain-5e9cc07a/RAP6mjwE5G00xYsA/oss/images/middleware_final.png?w=2500&fit=max&auto=format&n=RAP6mjwE5G00xYsA&q=85&s=437f141d1266f08a95f030c2804691d9)

Middleware flow diagram
