# Parallel Branches & Fan-Out

**Core Definition:** Routing execution to multiple nodes simultaneously.

## How to Fan-Out
You simply add multiple edges from the same source node.

### 1. Unconditional Fan-Out
"After A, run both B and C."

```python
workflow.add_edge("A", "B")
workflow.add_edge("A", "C")
```

### 2. Conditional Fan-Out
"Return a LIST of nodes to run."

```python
def parallel_router(state):
    return ["B", "C"] # Both will run!

workflow.add_conditional_edges("A", parallel_router)
```

## The "Send" API (Dynamic Fan-Out)
What if you want to run the *same* node 5 times on different data (Map-Reduce)?
Standard edges can't do this. You need `Send`.

```python
from langgraph.constants import Send

def map_router(state):
    return [
        Send("worker_node", {"item": i}) 
        for i in state["items"]
    ]

workflow.add_conditional_edges("planner", map_router)
```

## State Safety
When B and C run in parallel, they both try to update the State.
-   **Dicts:** If B updates key `b` and C updates key `c`, they merge fine.
-   **Lists:** If both append to `messages` (annotated with `add`), both messages appear (order indeterminate).
-   **Collisions:** If both write to key `x` (overwrite), one will win (race condition). **Avoid this.**

## Quick Summary

**1-Line Recall:** **Fan-Out happens when multiple edges originate from one node; use the `Send` API for dynamic mapping over a list.**
