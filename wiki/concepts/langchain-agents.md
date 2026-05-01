---
title: "LangChain Agents"
type: concept
tags: [langchain, agents, llm, tools, orchestration, reasoning]
created: 2026-05-01
updated: 2026-05-01
sources: ["raw/langchain-custom-middleware.md", "raw/langchain-middleare-overview.md"]
confidence: high
---

## Definition

LangChain agents are LLM-powered systems that autonomously decide which tools to use and in what order to accomplish a goal. Built with `create_agent()`, they follow an execution loop: call model → model selects tools → execute tools → repeat until model returns final answer. Agents differ from chains (pre-defined sequences) by making runtime decisions about tool usage.

## How It Works

**Core agent loop:**
1. **User input**: Provide messages and goal to agent
2. **Model call**: LLM receives conversation history, system prompt, available tools
3. **Tool selection**: Model returns tool calls (function name + arguments) or final answer
4. **Tool execution**: If tools selected, execute them and add results to conversation
5. **Repeat**: Loop back to step 2 with updated conversation
6. **End**: Model returns final answer with no tool calls

**Agent creation:**
```python
from langchain.agents import create_agent

agent = create_agent(
    model="gpt-5.4",           # LLM to use
    tools=[...],               # Available tools
    system_prompt="...",       # Instructions for agent
    middleware=[...],          # Cross-cutting concerns
)
```

**State management:**
- Agent maintains conversation state (messages list)
- Middleware can extend state with custom fields
- State updates flow through reducers for predictable merging

## Key Parameters

- **Model**: LLM selection (OpenAI, Anthropic, etc.) via model string or instance
- **Tools**: List of callable tools (Python functions, LangChain tools, API wrappers)
- **System prompt**: Instructions guiding agent behavior and tool usage
- **Middleware**: List of middleware for logging, retries, guardrails, etc.
- **State schema**: Optional extended state for custom fields
- **Checkpointer**: Storage backend for conversation persistence

## When To Use

- Multi-step tasks requiring dynamic tool selection
- Complex workflows where tool sequence depends on intermediate results
- Open-ended problems where solution path isn't known upfront
- Combining multiple APIs, databases, or services in flexible ways
- Tasks requiring reasoning about which tool to use when
- Iterative problem-solving (try tool, evaluate result, try another)
- Production systems needing reliability features (checkpointing, retries, observability)

## Risks & Pitfalls

- **Infinite loops**: Agent may repeatedly call same failing tool - implement call limits via middleware
- **Hallucinated tool calls**: Model invents non-existent tools or parameters - validate tool calls
- **Cost explosion**: Many tool iterations consume tokens rapidly - set budget limits
- **Slow execution**: Each model call adds latency - optimize prompts, use faster models for simple steps
- **Tool selection errors**: Model chooses wrong tool for task - improve tool descriptions and examples
- **State corruption**: Poorly designed reducers cause lost updates or inconsistent state
- **Security**: Agent may call dangerous tools with user-influenced parameters - validate inputs, sandbox tools
- **Reliability**: Production agents need error handling, retries, human-in-the-loop - use middleware

## Related Concepts

- [[concepts/autonomous-agents]] - Broader agent category
- [[concepts/langgraph]] - Graph-based agent orchestration
- [[concepts/middleware-pattern]] - Cross-cutting concerns
- [[concepts/tool-selection]] - Dynamic tool filtering
- [[concepts/prompt-engineering]] - Crafting effective agent prompts
- [[concepts/state-management]] - Managing agent execution state

## Sources

- raw/langchain-custom-middleware.md - Middleware for agent customization
- raw/langchain-middleare-overview.md - Agent loop and middleware integration
