# Dynamic vs Static Graphs

**Core Definition:**
-   **Static Graph:** The topology (nodes/edges) is defined *before* execution starts.
-   **Dynamic Graph:** The topology changes *during* execution (e.g., creating new nodes on the fly).

**LangGraph Stance:** LangGraph is fundamentally a **Static Graph** engine (mostly). You define the shape at compile time.

## Why Static?

1.  **Predictability:** The engine knows exactly what *can* happen.
2.  **Visualization:** You can draw the diagram before running it.
3.  **Persistence:** Checkpointing is easier when the structure is fixed.

## "Simulating" Dynamics

Even though the shape is static, the *path* is dynamic.
-   **Conditional Edges** allow for infinite variations of flow.
-   **Map-Reduce (Send API):**
    -   *Scenario:* A user asks 5 questions. You want to spawn 5 workers.
    -   *Graph Theory:* This looks like creating 5 nodes dynamically.
    -   *LangGraph:* We use the `Send()` API to route execution to the *same* node 5 times in parallel.

## Dynamic Node Creation (Advanced)

LangGraph *can* support truly dynamic graphs if you rebuild the `StateGraph` object inside a loop, but this is an anti-pattern for 99% of use cases.
-   **Better Pattern:** Use a Supervisor to delegate tasks to a fixed set of workers, or use `Send()` to parallelize over a list.

## Quick Summary

**1-Line Recall:** **LangGraph topology is static (defined at build time), but execution flow is dynamic (router logic and parallel branching).**
