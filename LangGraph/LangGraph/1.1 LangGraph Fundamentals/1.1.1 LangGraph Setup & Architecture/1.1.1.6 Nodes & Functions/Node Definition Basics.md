# Node Definition Basics

**Core Definition:** In LangGraph, a **Node** is simply a Python function. There is no special "Node Class" you must inherit from.

## The Mental Model
A Node is a **State Transformer**.
-   **Input:** Current State.
-   **Output:** Updates to the State.

## Minimal Example

```python
def my_node(state):
    return {"key": "new_value"}
```

## Naming Conventions
-   Use **snake_case** (e.g., `generate_summary`, `check_safety`).
-   Structure names as **Verb-Noun** (Action + Object) to clarify intent.
    -   *Good:* `validate_input`, `call_search_tool`.
    -   *Bad:* `processor`, `node_1`.

## Registering Nodes
You define the function first, then add it to the graph with a string label.

```python
# Definition
def agent(state):
    ...

# Registration
workflow.add_node("agent", agent)
```

**Note:** The string name `"agent"` is how you refer to this node in edges (`workflow.add_edge("agent", "tool")`).

## Quick Summary

**1-Line Recall:** **A node is just a Python function that takes `state` and returns `updates`, registered to the graph with a unique string name.**
