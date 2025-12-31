# Graph Execution Order

**Core Definition:** The rules determining which node runs next, especially when multiple paths exist.

**LangGraph Model:**
LangGraph executes in **Supersteps**.
-   **Step 1:** Run all "ready" nodes (usually just START).
-   **Step 2:** Process edges to find next "ready" nodes.
-   **Step 3:** Run all those nodes in parallel (if multiple).
-   **Repeat.**

## Sequential Execution
`A -> B -> C`
1.  **Superstep 1:** A runs.
2.  **Superstep 2:** B runs.
3.  **Superstep 3:** C runs.

## Parallel Execution
`A -> B` AND `A -> C`
1.  **Superstep 1:** A runs.
2.  **Superstep 2:** B AND C run **concurrently**.
    -   *Implementation:* They run in separate threads (or asyncio tasks).
    -   *State Update:* Since state is immutable/versioned, B and C can both write to the state. The "Reducer" function determines how their updates merge (e.g., append to list).

## Conditional Execution
`A -> (Router)`
-   If A returns "Go Left", B becomes ready.
-   If A returns "Go Right", C becomes ready.
-   *The "Router" itself is usually instant; it's just logic on the edge.*

## Priority and Race Conditions
LangGraph manages race conditions via the **Reducer**.
-   If B writes `x=1` and C writes `x=2`, and the reducer is `last_one_wins`, then execution order matters heavily.
-   If the reducer is `add` (append to list), then you get `[1, 2]` or `[2, 1]` (order indeterminate in parallel).

## Quick Summary

**1-Line Recall:** **Nodes run in discrete "Supersteps"; if multiple nodes are triggered at once, they run in parallel, and their outputs are merged by the State Reducer.**
