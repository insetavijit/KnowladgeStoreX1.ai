# Concurrent State Updates

**Core Definition:** What happens when two nodes write to the state at the exact same time (Parallel Branching).

## The Conflict
-   Node A: `return {"cnt": 1}`
-   Node B: `return {"cnt": 2}`

## Resolution Logic
1.  **Standard Keys:** Last write wins (Non-deterministic! Avoid this).
2.  **Annotated Keys (`operator.add`):** Both are preserved.
    -   `cnt: Annotated[list, add]`
    -   Result: `{"cnt": [1, 2]}` (Order is indeterminate).

## Atomic Updates (Not supported)
LangGraph does not support "read-modify-write" transactions across parallel nodes.
-   You cannot safely say `state["x"] += 1` in two parallel nodes and expect `x` to increase by 2, UNLESS you use a reducer.

## Best Practice for Parallelism
Have parallel nodes write to **separate keys** (`result_a`, `result_b`) or append to a **shared list**. Never have them overwrite the same scalar value.

## Quick Summary

**1-Line Recall:** **In parallel branches, avoid overwriting the same scaler key; use separate keys or 'Append' reducers to safely capture output from multiple nodes.**
