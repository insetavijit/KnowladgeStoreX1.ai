# Organizing Nodes

**Core Definition:** Strategies for structuring the functions that serve as **Nodes** in your LangGraph.

**The Problem:** Nodes contain the business logic. If you dump them all in one file, you get "Spaghetti Code."

## Strategies

### 1. Functional Grouping (By Role)
Group nodes based on what they *do*.
-   `src/nodes/retrieval.py`: All search/RAG nodes.
-   `src/nodes/generation.py`: All LLM generation nodes.
-   `src/nodes/validation.py`: All grading/checking nodes.

### 2. Domain Grouping (By Feature)
Group nodes based on the *feature* they support.
-   `src/features/onboarding/nodes.py`
-   `src/features/support/nodes.py`

### 3. The `__init__.py` Pattern
Expose nodes cleanly so the graph definition stays readable.

```python
# src/nodes/__init__.py
from .retrieval import retrieve_documents
from .generation import generate_answer

__all__ = ["retrieve_documents", "generate_answer"]
```

Then in `graph.py`:
```python
from src.nodes import retrieve_documents, generate_answer
```

## Stateless vs Stateful

-   **Pure Functions:** Most nodes should be pure functions of `(state) -> update`. Keep side effects (like database writes) isolated if possible or clearly marked.

## Quick Summary

**1-Line Recall:** **Don't dump nodes in `graph.py`; group them in a `nodes/` module by functionality to keep the graph definition clean.**
