# Graph Basics

**Core Definition:** A network of nodes (functions) connected by edges (control flow), centered around a shared, persistent state.

## The Mental Model
A **State Machine**. The agent is in a "State", performs an action, and transitions to a new "State".

## Syntax (LangGraph)
You explicitly define nodes and edges.

```python
workflow = StateGraph(State)
workflow.add_node("agent", agent_node)
workflow.add_node("tools", tool_node)
workflow.add_edge("tools", "agent") # Loop!
```

## Characteristics
1.  **Stateful:** The `State` object persists and evolves across steps.
2.  **Explicit Control:** You define exactly where data goes next.
3.  **Cyclic:** Loops are a first-class feature.

## Quick Summary

**1-Line Recall:** **Graphs are cyclic, stateful architectures where nodes read/write to a shared memory schema, enabling complex agentic behaviors.**
