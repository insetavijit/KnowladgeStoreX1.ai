# Edge Types

**Core Definition:** Edges represent the transition of control from one node to another. They define the "Topology" of the graph.

## Everything is an Edge
In LangGraph, there is no "next line of code." If control moves from A to B, an **Edge** MUST exist.

## The Two Main Types

### 1. Normal (Unconditional) Edges
"After Node A finishes, **ALWAYS** go to Node B."
-   **Symbol:** Solid Arrow `-->`
-   **Usage:** Building linear sequences/chains.
-   **Determinism:** 100%.

### 2. Conditional Edges
"After Node A finishes, check the State (or Output), run some logic, and **DECIDE** where to go."
-   **Symbol:** Diamond/Decision `--> <> -->`
-   **Usage:** If/Else logic, Loops, Tool calls.
-   **Determinism:** Dependent on the routing logic (can be probabilistic if based on LLM output).

## The Implicit Edges
-   **START Edge:** The one edge that points FROM `START` to your first node.
-   **END Edge:** Any edge pointing TO `END`.

## Naming Edges
Edges generally don't have "names" themselves, but **Conditional Edges** are often named after the function that defines them (e.g., `shoulder_continue`).

## Quick Summary

**1-Line Recall:** **Edges come in two flavors: Unconditional (Always Go) and Conditional (Decide Then Go); they are the only way to move control forward.**
