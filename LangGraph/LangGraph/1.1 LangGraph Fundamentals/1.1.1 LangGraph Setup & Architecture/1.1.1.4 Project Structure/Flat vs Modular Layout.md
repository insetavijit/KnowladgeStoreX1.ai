# Flat vs Modular Layout

**Core Definition:** The architectural choice between keeping all code in a single file/folder (Flat) versus separating concerns into dedicated directories (Modular).

**The Concept:**
-   **Flat:** Great for prototypes, tutorials, and scripts under 200 lines.
-   **Modular:** Essential for production agents, teams, and long-term maintenance.

## Comparison

| Feature | Flat Layout | Modular Layout |
| :--- | :--- | :--- |
| **Speed** | Fast to start | Slower setup |
| **Cognitive Load** | High (one giant file) | Low (focused modules) |
| **Reusability** | Poor (copy-paste code) | High (import shared modules) |
| **Testing** | Hard (mocking is difficult) | Easy (test individual units) |

## When to Switch?

Move from Flat to Modular when:
1.  Your `graph.py` exceeds 300 lines.
2.  You have more than 3 custom tools.
3.  You need to share nodes between two different graphs.
4.  You start writing unit tests.

## LangGraph Specifics

In **Flat** mode:
```python
# app.py
def node_a(state): ...
def node_b(state): ...
workflow = StateGraph(State)
workflow.add_node("a", node_a)
```

In **Modular** mode:
```python
# graph.py
from src.nodes import node_a, node_b
from src.state import State

workflow = StateGraph(State)
workflow.add_node("a", node_a)
```

## Quick Summary

**1-Line Recall:** **Start flat for speed, but refactor to modular structure before your first production deployment.**
