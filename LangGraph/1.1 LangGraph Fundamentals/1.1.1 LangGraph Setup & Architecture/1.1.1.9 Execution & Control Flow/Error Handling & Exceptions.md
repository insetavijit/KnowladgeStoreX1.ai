# Error Handling & Exceptions

**Core Definition:** How exceptions propagate and how to catch them at the graph level.

## Default Behavior: Crash
If a node raises an unhandled exception (and retries are exhausted), the `invoke()` call raises that exception in Python. The graph execution aborts.

## Handling in Nodes (Try/Catch)
The best place to handle logic errors (parsers failing) is *inside* the node. Return an error flag in the state instead of raising.

```python
def node(state):
    try:
        ...
    except ValueError as e:
        return {"error": str(e)}
```

## Handling in Edges
Use conditional edges to check for that error flag.
```python
if state.get("error"): return "error_handler_node"
```

## Recovering from a Crash
If the graph crashes due to a bug:
1.  Fix the bug in the code.
2.  Use "Time Travel" to update the state (fix the bad data).
3.  Resume the thread. The new code runs.

## Quick Summary

**1-Line Recall:** **Unhandled exceptions crash the graph execution; prefer catching errors in nodes and returning error states to route to recovery paths.**
