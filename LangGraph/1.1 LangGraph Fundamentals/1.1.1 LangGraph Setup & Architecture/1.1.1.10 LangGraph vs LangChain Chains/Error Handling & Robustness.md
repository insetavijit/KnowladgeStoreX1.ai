# Error Handling & Robustness

**Core Definition:** What happens when things break.

## Chains: Crash Propagation
If a step in a chain fails, the whole chain usually raises the exception.
-   You can wrap the whole chain in a `try/except`, but you lose the intermediate progress.

## Graphs: Edges of Resilience
You can define specific error handling *paths*.

```python
def route_error(state):
    if state["error"]:
        return "fallback_node"
    return "next_node"
```

-   **Recovery:** If a tool fails, you can route to a node that says "Tool failed, trying alternative..." and then loops back.
-   **Durability:** The state is checkpointed. If it crashes, you can fix the bug and resume from the crash point.

## Quick Summary

**1-Line Recall:** **Graphs allow you to model 'failure' as just another valid state transition, enabling sophisticated recovery workflows.**
