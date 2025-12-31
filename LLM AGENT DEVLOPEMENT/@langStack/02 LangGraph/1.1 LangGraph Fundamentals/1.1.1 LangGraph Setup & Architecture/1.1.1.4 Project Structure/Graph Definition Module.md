# Graph Definition Module

**Core Definition:** The module where you instantiate `StateGraph`, add nodes, draw edges, and compile the application.

**Role:** This is the "wiring diagram" of your application. It should contain *structure*, not *logic*.

## Best Practice: `src/graph.py`

Keep this file focused on the `.add_node()` and `.add_edge()` calls.

```python
# src/graph.py
from langgraph.graph import StateGraph, END
from src.state import AgentState
from src.nodes import node_a, node_b
from src.Checkpointer import memory

# 1. Init
workflow = StateGraph(AgentState)

# 2. Add Nodes
workflow.add_node("node_a", node_a)
workflow.add_node("node_b", node_b)

# 3. Add Edges
workflow.set_entry_point("node_a")
workflow.add_edge("node_a", "node_b")
workflow.add_edge("node_b", END)

# 4. Compile
graph = workflow.compile(checkpointer=memory)
```

## The Factory Pattern

For larger apps, wrap the creation in a function. This lets you pass in configuration (like a different Checkpointer for testing).

```python
def create_graph(checkpointer=None):
    workflow = StateGraph(AgentState)
    # ... wiring ...
    return workflow.compile(checkpointer=checkpointer)
```

## Quick Summary

**1-Line Recall:** **`graph.py` is the wiring diagram; it should import nodes and connect them, but contain zero business logic itself.**
