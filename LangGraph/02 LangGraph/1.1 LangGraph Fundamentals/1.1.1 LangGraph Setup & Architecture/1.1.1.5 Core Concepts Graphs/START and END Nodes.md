# START and END Nodes

**Core Definition:** The special virtual nodes that define the entry and exit points of a LangGraph workflow.

## The `START` Node

-   **Symbol:** `langgraph.graph.START`
-   **Role:** The entry point. When you call `graph.invoke(input)`, the `input` is injected at the `START` node.
-   **Wiring:** You must define where the graph begins by adding an edge from `START` to your first real node.
    ```python
    workflow.add_edge(START, "first_node")
    ```
    *Alternative syntax: `workflow.set_entry_point("first_node")`*

## The `END` Node

-   **Symbol:** `langgraph.graph.END`
-   **Role:** The termination signal. When execution reaches `END`, the graph stops and returns the final state.
-   **Wiring:** Any node can point to `END`.
    ```python
    # After 'publish', stop.
    workflow.add_edge("publish", END)
    
    # Conditional logic
    def router(state):
        if state["is_finished"]:
            return END
        return "continue_node"
    ```

## Properties

### 1. Multiple Ends
A graph can have many paths to `END`.
-   Success Path: `... -> Generate -> END`
-   Failure Path: `... -> ErrorHandler -> END`

### 2. Single Start
A graph currently has one logical entry point for a single run, though advanced patterns (subgraphs) can behave like they have multiple entries depending on how they are called.

### 3. Reachability Rule
A valid graph compilation requires:
1.  All nodes must be reachable from `START`.
2.  All nodes must eventually have a path to `END` (no infinite traps, though the compiler can't prove finite loops).
3.  Dead-end nodes (nodes with no outgoing edges) are compilation errors unless they are meant to be terminal (in which case, route them to `END`).

## The `__end__` Key
In the final output dictionary of a graph execution, you generally just get the state. However, internally, the system treats `__end__` as the signal that the generator is exhausted.

## Quick Summary

**1-Line Recall:** **START initializes the state with user input; END returns the final state to the user; every valid path must connect the two.**
