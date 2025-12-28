# LangChain Expression Language (LCEL)

**Core Definition:** The pipe syntax `|` for chaining runnables.

## Graphs use LCEL
They are not enemies!
-   **Nodes** in LangGraph are often LCEL chains.

```python
# Create an LCEL chain
chain = prompt | model | parser

# Use it as a Node
workflow.add_node("generator", chain)
```

## Composition
LangGraph orchestrates the *Macro* architecture (loops, branching).
LCEL orchestrates the *Micro* architecture (linear steps inside a node).

## Quick Summary

**1-Line Recall:** **LCEL and LangGraph are complementary; use LCEL to define the logic *inside* a node, and LangGraph to define the flow *between* nodes.**
