# Documentation & Examples

**Core Definition:** The files that tell other humans (and your future self) how to use the project.

**The Minimum Viable Docs:**
1.  **README.md**: What is it? How do I run it?
2.  **ARCHITECTURE.md**: Visual diagram of the graph.
3.  **examples/**: Runnable scripts.

## The `examples/` Directory

Don't just write code blocks in the README. Create actual python files that work.

```python
# examples/basic_chat.py
from src.graph import graph

print("Running Basic Chat Example...")
graph.invoke({"messages": [("user", "Hello!")]})
```

**Why?** Because you can add these examples to your CI pipeline to ensure your documentation never goes stale.

## Automating Graph Diagrams

LangGraph can draw itself. Include a script to update your architecture diagram automatically.

```python
# scripts/draw_graph.py
from src.graph import graph

png_bytes = graph.get_graph().draw_mermaid_png()
with open("docs/architecture.png", "wb") as f:
    f.write(png_bytes)
```

## Quick Summary

**1-Line Recall:** **Treat documentation as code; keep runnable examples in `examples/` and test them in CI.**
