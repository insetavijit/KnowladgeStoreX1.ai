# Merging Paths & Fan-In

**Core Definition:** Bringing parallel branches back together into a single stream of execution.

## How to Fan-In
You simply point multiple edges to the same destination node.

```python
workflow.add_edge("B", "D")
workflow.add_edge("C", "D")
```

## Synchronization (The Barrier)
LangGraph treats this as a **Barrier**.
-   Node D will NOT run until **ALL** active incoming paths have finished.
-   If B finishes in 1s and C takes 10s, D waits 10s.

## The "Reducer" Logic
When B and C finish, their outputs are merged into the state *before* D runs.
-   **Node B:** `return {"score_b": 10}`
-   **Node C:** `return {"score_c": 20}`
-   **State at D:** `{"score_b": 10, "score_c": 20, ...}`

## Deadlocks
Be careful with Conditional Fan-Out.
-   If A routes to B (but skips C), and D waits for B *and* C...
-   Actually, LangGraph is smart. It knows C was never activated, so D only waits for B.
-   However, logic errors where a branch "crashes" but doesn't report status can leave D waiting indefinitely (rare in Python, common in distributed systems).

## Quick Summary

**1-Line Recall:** **Fan-In acts as a synchronization barrier; the target node waits for all active upstream branches to complete before executing.**
