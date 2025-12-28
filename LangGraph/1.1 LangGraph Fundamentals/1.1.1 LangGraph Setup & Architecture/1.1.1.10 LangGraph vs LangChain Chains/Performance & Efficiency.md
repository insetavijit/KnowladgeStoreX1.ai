# Performance & Efficiency

**Core Definition:** Latency and Overhead.

## Chains: Low Overhead
-   Very fast construction.
-   Minimal function call overhead (just piping data).
-   **Limit:** Hard to parallelize effectively without relying on `RunnableParallel`.

## Graphs: Medium Overhead
-   State merging adds microseconds.
-   Checkpointing adds milliseconds (db writes).
-   **Win:** Massive parallelization gains. You can fan-out to 50 nodes easily, which outweighs the localized overhead.

## Streaming
Both support streaming, but LangGraph's event stream (`stream_mode="updates"`) is often richer, providing structural updates rather than just token streams.

## Quick Summary

**1-Line Recall:** **Chains are slightly faster for single-threaded tasks, but Graphs unlock massive concurrency gains for complex parallel workloads.**
