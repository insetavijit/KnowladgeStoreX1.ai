# Dynamic Routing

**Core Definition:** When the *destination* of an edge isn't known until runtime, often chosen by an LLM.

## The "Registry" Pattern
Instead of hardcoding standard nodes, you might load plugins dynamically.

```python
PLUGIN_REGISTRY = {
    "weather": weather_node,
    "stock": stock_node,
    "news": news_node
}

def plugin_router(state):
    plugin_name = state["selected_plugin"]
    if plugin_name in PLUGIN_REGISTRY:
        return plugin_name
    return "error"
```

## LLM-Driven Routing
The most common dynamic pattern.
1.  **Prompt:** "Analyze the user query and pick the best expert: [A, B, C]."
2.  **LLM Output:** "B"
3.  **Router:** Returns "B".

## Constraints
Even in "Dynamic" routing, the target nodes must technically exist in the compiled graph. You can't route to a function that wasn't added via `.add_node()` (unless you use advanced subgraph compilation at runtime, which is rare).

## Quick Summary

**1-Line Recall:** **Dynamic Routing leverages the LLM's cognition to select a path from the available nodes, giving the agent "Choice".**
