# Looping with Edges

**Core Definition:** Creating a **Cycle** by defining an edge that points to a node that has already executed.

## The Syntax of a Loop
There is no `while` loop syntax in LangGraph. You just point backwards.

```python
# Unconditional Loop (Runs until recursion limit)
workflow.add_edge("node_b", "node_a")

# Conditional Loop (The Standard)
def check_loop(state):
    if state["is_finished"]:
        return END
    return "node_a"

workflow.add_conditional_edges("node_b", check_loop)
```

## Common Loop Patterns

### 1. The Tool Loop
`Agent -> Tools -> Agent`
-   The Agent calls a tool.
-   The Tool runs.
-   The graph loops back to the Agent with the tool output.
-   The Agent decides "I'm done" and routes to END.

### 2. The Refinement Loop
`Draft -> Critique -> Draft`
-   Generate a draft.
-   Critique it.
-   If critique passes -> END.
-   If critique fails -> Loop back to Draft (with feedback).

## Recursion Limits
Cycles are dangerous. LangGraph protects you with `recursion_limit` (default 25).
-   If your loop hits 25 steps, it crashes with `RecursionLimitError`.
-   **Config:** `graph.invoke(..., config={"recursion_limit": 100})`.

## Quick Summary

**1-Line Recall:** **Loops are just edges pointing backwards; always gate them with a conditional check to prevent infinite execution.**
