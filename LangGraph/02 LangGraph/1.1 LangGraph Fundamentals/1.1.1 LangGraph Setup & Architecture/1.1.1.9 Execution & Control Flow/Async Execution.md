# Async Execution

**Core Definition:** Running graphs in an `asyncio` loop. This is required for high-performance web servers (FastAPI).

## Why Async?
If you use `invoke()` inside a FastAPI route, you block the entire server process while waiting for OpenAI (which takes seconds). `async` allows the server to handle other requests while waiting.

## Syntax
Everything is the same, just add `a`.

```python
# Create graph
graph = workflow.compile()

# Run it
final_state = await graph.ainvoke(inputs)

# Stream it
async for event in graph.astream(inputs):
    print(event)
```

## Async Nodes
Ideally, your nodes should also be `async def`.
If you use `ainvoke` with synchronous `def` nodes, LangGraph (and LangChain) runs them in a thread pool to avoid blocking the loop.

## Quick Summary

**1-Line Recall:** **Always use `ainvoke` and `astream` in web applications to maintain server throughput; it natively awaits async nodes.**
