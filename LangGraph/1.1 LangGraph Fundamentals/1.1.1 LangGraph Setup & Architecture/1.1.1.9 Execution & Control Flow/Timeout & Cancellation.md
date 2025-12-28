# Timeout & Cancellation

**Core Definition:** Ensuring graphs don't run forever or get stuck.

## Infinite Loops
LangGraph has a built-in `recursion_limit` (default 25).
```python
graph.invoke(inputs, {"recursion_limit": 100})
```
If the graph steps 100 times without ending, it raises an error.

## Step Timeout
There is no global "timeout" parameter for `invoke` in the open-source library (besides standard async cancellation).
-   You should wrap `await graph.ainvoke()` in `asyncio.wait_for(..., timeout=30)`.

## Cancellation
In async contexts, if you cancel the `task`, LangGraph stops.
-   Because state is checkpointed at every step, the execution is effectively "Paused". You can resume it later or abandon it.

## Quick Summary

**1-Line Recall:** **Use `recursion_limit` to prevent infinite logical loops and `asyncio` timeouts to limit wall-clock execution time.**
