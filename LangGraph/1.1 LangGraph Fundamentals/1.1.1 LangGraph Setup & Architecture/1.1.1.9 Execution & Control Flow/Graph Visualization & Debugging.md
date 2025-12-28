# Graph Visualization & Debugging

**Core Definition:** Tools to see the topology and flow of your graph.

## Mermaid / ASCII
LangGraph compiles to a `Runnable` that has a `.get_graph()` method.

```python
# Print ASCII art
print(graph.get_graph().draw_ascii())

# Get Mermaid syntax (for markdown/UIs)
print(graph.get_graph().draw_mermaid())

# Save as PNG (requires graphviz)
graph.get_graph().draw_mermaid_png(output_file_path="graph.png")
```

## State Inspection
During debugging, you often want to see "What is the state right now?".
```python
state = graph.get_state(config)
print(state.values)
print(state.next) # What node is next?
```

## Quick Summary

**1-Line Recall:** **Use `graph.get_graph().draw_mermaid()` to visualize your agent's topology; use `graph.get_state()` to inspect memory during pauses.**
