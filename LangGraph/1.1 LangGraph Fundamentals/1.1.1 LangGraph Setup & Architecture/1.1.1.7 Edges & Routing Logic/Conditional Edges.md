# Conditional Edges

**Core Definition:** The mechanism for **Dynamic Routing**. It allows the graph to branch based on data.

## Syntax
```python
workflow.add_conditional_edges(
    "source_node",      # 1. Where do we start?
    routing_function,   # 2. What logic do we run?
    path_map            # 3. (Optional) Mapping of outputs to node names
)
```

## The Routing Function
This function receives the State and returns a String (the name of the next node).
```python
def decide_mood(state):
    if "happy" in state["user_input"]:
        return "happy_node"
    return "sad_node"
```

## The Path Map (Optional but Recommended)
A dictionary mapping the function's output strings to the actual node names.
-   **Why?** It validates your graph structure at compile time.
-   **Syntax:**
    ```python
    workflow.add_conditional_edges(
        "classifier",
        decide_mood,
        {
            "happy_node": "happy_node",
            "sad_node": "sad_node"
        }
    )
    ```
    *Note: If keys and values are identical, you can sometimes omit the map in newer versions, but explicit is better.*

## The "End" Case
Conditional edges are the primary way to route to `END`.
```python
return END  # Imported from langgraph.graph
```

## Quick Summary

**1-Line Recall:** **Conditional Edges use a Python function to inspect state and return the name of the destination node, enabling branching logic.**
