# Paths & Reachability

**Core Definition:** A **Path** is a sequence of edges connecting a sequence of nodes. **Reachability** asks: "Is it possible to get from Node A to Node B?"

**Why it Matters:** A broken path means your agent crashes or gets stuck.

## Graph Traversal Logic

When LangGraph executes:
1.  Current Node finishes.
2.  System checks Outgoing Edges.
    -   **One Edge:** Follow it.
    -   **Conditional Edge:** Run the function -> get destination -> Follow it.
    -   **No Edge:** Error (unless END).

## Reachability Problems

### 1. Unreachable Nodes (Orphans)
A node exists in the code but no edge points TO it.
-   *Symptom:* You wrote the code, but it never runs.
-   *Fix:* Check your `.add_edge()` logic.

### 2. Dead Ends (Sinks)
A node has no way to get to `END`.
-   *Symptom:* `GraphValidationError` at compile time.
-   *Fix:* Ensure every branch eventually routes to `END`.

### 3. Infinite Traps
A cycle with no exit condition.
-   *Symptom:* `RecursionLimitError`.
-   *Fix:* Ensure your router has a `count > limit` check.

## Analyzing Paths

LangGraph Studio visualizes paths.
-   **Happy Path:** The sequence of nodes for a successful run.
-   **Edge Case Path:** The sequence when errors occur (e.g., `ToolError -> Retry -> Tool`).

## Quick Summary

**1-Line Recall:** **A valid graph must have a Path from START to every node, and from every node to END.**
