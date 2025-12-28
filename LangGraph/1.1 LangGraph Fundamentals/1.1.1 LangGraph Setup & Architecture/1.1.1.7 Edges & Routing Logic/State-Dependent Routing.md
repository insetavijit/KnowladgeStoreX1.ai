# State-Dependent Routing

**Core Definition:** Edges that look purely at the data in `GraphState` (variables, counters, flags) rather than just the output of the last node.

## Context vs. Output
-   **Output Routing:** Node A returns "success", so go to B.
-   **State Routing:** Node A returns nothing, but `state["user_tier"]` is "gold", so router sends to B.

## Utilizing History
You can route based on what happened 5 steps ago.
```python
def check_history_router(state):
    # If we already tried "search" twice, don't try it again
    search_count = sum(1 for m in state["messages"] if m.name == "search")
    if search_count > 2:
        return "give_up"
    return "search"
```

## Global Flags
Using a shared "Context" object inside state is best practice for routing.
-   `state["is_debug_mode"]`
-   `state["language"]`

These allow you to change the flow of the entire graph by flipping one switch in the input.

## Quick Summary

**1-Line Recall:** **Routers have access to the *entire* history of the conversation, allowing for decisions based on long-term context (loops, total cost, etc.).**
