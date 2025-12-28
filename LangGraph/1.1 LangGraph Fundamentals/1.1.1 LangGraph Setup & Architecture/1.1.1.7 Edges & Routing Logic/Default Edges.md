# Default Edges

**Core Definition:** Handling the "else" case in routing to prevent crashes.

## The Problem
If your routing function returns `"unknown_node"`, the graph crashes.

## Best Practice: Explicit Defaults
Always return a safe fallback string in your router.

```python
def router(state):
    choice = state["choice"]
    if choice == "A": return "node_a"
    if choice == "B": return "node_b"
    
    # The Default
    return "node_default" 
```

## "Pass-Through" Defaults
Sometimes, if the condition isn't met, you just want to continue linearly.

```python
# Check for tool calls, otherwise go to END
def router(state):
    if state["tool_calls"]:
        return "tools"
    return END
```
Here, `END` is the default.

## Graph Validation
When you call `workflow.compile()`, LangGraph checks if all possible return values from your conditional edges map to real nodes.
-   *Tip:* This is why providing the `path_map` dictionary to `add_conditional_edges` is helpful—it acts as documentation for what the permitted defaults are.

## Quick Summary

**1-Line Recall:** **Always program a default return value in your routers to ensure the graph never attempts to route to a non-existent node.**
