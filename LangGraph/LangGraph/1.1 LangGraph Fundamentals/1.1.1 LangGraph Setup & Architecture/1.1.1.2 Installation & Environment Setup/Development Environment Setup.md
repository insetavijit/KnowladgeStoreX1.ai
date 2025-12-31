# Development Environment Setup

**Core definition:** Configuring your **IDE** (VS Code, PyCharm), **debugger**, and **linter** to make building graphs easier.

**Position in ecosystem:**
LangGraph code can get complex. Trying to debug a cyclic graph with just `print()` statements is pain.

**Key idea:**
- **VS Code Pylance:** Essential for auto-completing typed State objects.
- **Jupyter Notebooks:** Great for rapid prototyping of graphs (visualizing output steps).
- **Debugging:** Set breakpoints inside your node functions to inspect state.

## Recommended Tools

1.  **VS Code** + Python Extension.
2.  **Jupyter Lab:** `pip install jupyterlab`.
3.  **Black / Ruff:** For formatting code automatically.

## Debugging Tip
In `launch.json` (VS Code), set `"justMyCode": false` if you need to step into LangGraph library code to see why an edge isn't firing.

## Quick Summaries

**30-second version:** Don't write code in Notepad. Use VS Code with strict type checking enabled. LangGraph uses a lot of complex types (`TypedDict`, `Annotated`), and your IDE can save you hours of bug hunting by underlining mistakes before you even run the code.

**One-line recall:**
**Use an IDE with strong type-checking support (VS Code + Pylance).**

---

## Linked Concepts
- [[Testing Environment]]
- [[Troubleshooting Installation Issues]]
- [[API Key Management]]

---
**Last updated:** December 2025
