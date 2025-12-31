# Performance Optimization in Nodes

**Core Definition:** Making your nodes run faster and cheaper.

## 1. Parallelization (Async)
The biggest win. If you have 3 independent tools, run them in parallel.
-   **Method:** Use `async def` and `asyncio.gather` inside a node, OR use the Graph's built-in parallel branch execution.

## 2. Caching
Don't re-compute expensive things.
-   **LangChain Cache:** Use `set_llm_cache` to cache exact LLM repeats.
-   **Memoization:** Use `@functools.lru_cache` for pure logic nodes.

## 3. Projection (Batching)
If retrieving documents, don't retrieve full text if you only need headers first. Optimize the data payload in the State.

## 4. Latency Hiding (Streaming)
You can't make the LLM faster, but you can make it *feel* faster.
-   Stream the output of the node **while it is being generated**.
-   This requires your API/Frontend to consume the stream.

## Quick Summary

**1-Line Recall:** **Optimize by using Async I/O for network calls and caching for expensive pure computations; use Streaming to improve perceived latency.**
