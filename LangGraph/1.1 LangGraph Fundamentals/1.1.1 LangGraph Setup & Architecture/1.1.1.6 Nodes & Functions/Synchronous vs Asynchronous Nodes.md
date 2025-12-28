# Synchronous vs Asynchronous Nodes

**Core Definition:** Choosing between `def` (blocking) and `async def` (non-blocking) for your node functions.

## The Golden Rule
**If your node performs I/O (calls an LLM, Database, or API), make it ASYNC.**

## 1. Async Nodes (Recommended)
Allows Python to handle other concurrent requests while waiting for the LLM.

```python
async def call_model(state: State):
    # 'await' relinquishes control so the server stays responsive
    response = await llm.ainvoke(state["messages"])
    return {"messages": [response]}
```

## 2. Sync Nodes
Best for pure CPU logic (parsing JSON, basic math, string formatting).

```python
def parse_output(state: State):
    # No I/O here, just logic
    last_msg = state["messages"][-1]
    return {"parsed": json.loads(last_msg.content)}
```

## Mixing Sync and Async
LangGraph handles mixed graphs seamlessly.
-   If you run `graph.invoke()`, it runs everything synchronously (async nodes are run in a loop).
-   If you run `await graph.ainvoke()`, it runs async nodes natively and wraps sync nodes in headers.

## Performance Impact
Using `def` for an API call blocks the *entire thread*. In a web server (FastAPI), this kills throughput. Always use `async def` for network operations.

## Quick Summary

**1-Line Recall:** **Use `async def` for everything involving network/disk I/O to keep your agent responsive; mixing sync/async is fully supported.**
