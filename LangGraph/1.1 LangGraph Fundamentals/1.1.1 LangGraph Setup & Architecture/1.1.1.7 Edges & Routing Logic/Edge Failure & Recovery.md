# Edge Failure & Recovery

**Core Definition:** Routing logic designed specifically to handle node failures or exceptions.

## The "Crash" Scenario
If Node A raises an Exception, the graph stops. Edges allow us to "catch" this conceptually.

## Pattern 1: The Validation Loop
Node A produces output. Node B validates it. If invalid, Edge routes back to A.

```python
def validate_router(state):
    if state["validation_errors"]:
        return "rewrite_node" # Failure path
    return "publish_node"     # Success path
```

## Pattern 2: The Dead Letter Queue
If a node fails repeatedly (max retries hit), you might want to route to a manual review node instead of crashing.

This usually requires a **Fallback Node** that catches the exception and updates the state with a status like `{"status": "failed"}`. The router then sees this status:

```python
def status_router(state):
    if state["status"] == "failed":
        return "human_review"
    return "next_step"
```

## Pattern 3: Timeout Edges
(Advanced) If a parallel branch runs too long, a separate clock-watching branch could trigger a state update that forces the graph to move on.

## Quick Summary

**1-Line Recall:** **Use conditional edges to build "Self-Correcting" loops that route validation failures back to the generator or to a human fallback.**
