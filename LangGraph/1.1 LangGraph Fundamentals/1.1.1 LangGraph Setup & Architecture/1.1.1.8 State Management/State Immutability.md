# State Immutability

**Core Definition:** The principle that you never modify the `state` object in place; you create a NEW version of it.

## Graph State is Functional
LangGraph follows functional programming principles.
-   **Input:** Old State.
-   **Process:** Apply Update.
-   **Output:** New State.

## The Risk of Mutation
If you do this:
```python
def bad_node(state):
    state["count"] += 1 # Mutation!
    return {}
```
...you break the history tracking. The graph might not "see" the change, or checkpoints might capture the wrong version.

## Correct Pattern: Copy-on-Write (Implicit)
You don't literally have to clone the dict yourself. LangGraph handles the merging. You just return the *diff*.

```python
def good_node(state):
    return {"count": state["count"] + 1} # Return the new value
```

## Deep Mutability
Be careful with nested objects (lists/dicts). Even if you return a dict, if you modified a list *inside* the state in-place, you might cause issues in concurrent scenarios.

## Quick Summary

**1-Line Recall:** **Treat the `state` argument as read-only; express changes solely by returning a dictionary of updates.**
