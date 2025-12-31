# Error Handling in Nodes

**Core Definition:** How to prevent a single node failure from crashing the entire graph.

## 1. Try/Except Blocks
The first line of defense. Catch expected errors.

```python
def search_node(state):
    try:
        results = search_api.run(...)
    except Exception as e:
        # Don't crash; report failure
        return {"error": str(e)}
```

## 2. Retry Policies
LangGraph supports automatic retries on node execution.

```python
# Retry up to 3 times on any exception
workflow.add_node("search", search_node, retry=RetryPolicy(max_attempts=3))
```

## 3. Fallback Nodes
If a node fails permanently, route to a fallback.
*Note: This usually requires the node to capture the error and return a specific flag, which a Conditional Edge then sees.*

```python
def route_error(state):
    if state.get("error"):
        return "fallback_node"
    return "next_node"
```

## 4. The `Command` Exception
In newer versions, you can raise specific exceptions to trigger graph-level interruptions, but `try/catch` is preferred for business logic errors.

## Quick Summary

**1-Line Recall:** **Wrap risky Logic in try/except blocks and use LangGraph's `RetryPolicy` for transient network failures.**
