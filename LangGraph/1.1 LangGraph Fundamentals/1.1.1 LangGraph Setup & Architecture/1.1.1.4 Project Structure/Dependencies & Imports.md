# Dependencies & Imports

**Core Definition:** Managing the web of Python imports within your project to ensure stability, readability, and speed.

**The Golden Rule:** **Imports should flow Down, not Up or Sideways.**
Graph -> Nodes -> Tools -> Utils

## 1. Absolute Imports
Always prefer absolute imports using your package name.
-   **Good:** `from src.nodes.agent import agent_node`
-   **Bad:** `from ..nodes.agent import agent_node` (Hard to move files later)

## 2. Lazy Imports
For heavy dependencies (like `pandas` or `torch`), import them *inside* the function that needs them, not at the top of the file. This makes your CLI start faster.

```python
def analyze_data(state):
    import pandas as pd  # Lazy import
    # ...
```

## 3. The `__init__.py` Facade
Use `__init__.py` files to define the public API of a module.

```python
# src/nodes/__init__.py
# Only expose what other modules need to see
from .search import search_node
from .generate import generate_node
```

## 4. Managing `requirements.txt`
Split your dependencies:
-   `requirements.txt`: Prod dependencies (langgraph, openai).
-   `requirements-dev.txt`: Dev tools (pytest, black, ruff).

## Quick Summary

**1-Line Recall:** **Use absolute imports (`from src...`) and keep your dependency tree directional (Graph depends on Nodes, not vice versa).**
