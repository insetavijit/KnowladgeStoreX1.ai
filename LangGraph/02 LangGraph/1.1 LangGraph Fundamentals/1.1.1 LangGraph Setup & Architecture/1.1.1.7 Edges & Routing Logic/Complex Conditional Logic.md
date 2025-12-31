# Complex Conditional Logic

**Core Definition:** Handling multi-step or multi-variable decisions within edges.

## Multi-Way Branching
You aren't limited to `if/else` (2 paths). You can have 10 paths.

```python
def department_router(state):
    dept = state["department"]
    if dept == "hr": return "hr_node"
    if dept == "sales": return "sales_node"
    if dept == "eng": return "eng_node"
    return "general_node" # Always have a fallback
```

## Nested/Weighted Logic
Sometimes the decision depends on multiple factors.
*"If urgency is High OR (urgency is Medium AND customer is VIP), go to Human."*

```python
def escalation_router(state):
    if state["urgency"] == "high":
        return "human"
    if state["urgency"] == "medium" and state["is_vip"]:
        return "human"
    return "bot"
```

## State Mutation in Routers? (Anti-Pattern)
Technically, you *can* modify the state object passed to the router, but **IT WILL BE LOST.**
-   Routers DO NOT return state updates. They return strings.
-   If you need to change state (e.g., incrementing a counter), do it in the **Node** before the router.

## The "Unknown" Case
Robust systems always handle the "I don't know" case.
-   If the LLM outputs garbage that doesn't match any branch, route to a `fallback_node` or `error_node`.

## Quick Summary

**1-Line Recall:** **Routers can handle complex logic, but remember they are read-only; perform any necessary state mutations in the preceding node.**
