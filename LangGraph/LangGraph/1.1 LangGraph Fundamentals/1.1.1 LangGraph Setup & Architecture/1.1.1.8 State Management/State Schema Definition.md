# State Schema Definition

**Core Definition:** The blueprint of your graph. It defines exactly what data structure is passed between nodes.

## The `TypedDict` Standard
The most common way to define state in LangGraph is using Python's `TypedDict`.

```python
from typing import TypedDict, List

class GraphState(TypedDict):
    messages: List[str]
    user_id: str
    retry_count: int
    is_finished: bool
```

## Why Type Hints Matter
1.  **IDE Autocomplete:** When writing nodes, you know exactly what keys exist.
2.  **Runtime Validation:** LangGraph uses the schema to valid state updates (partially) and for serialization.
3.  **Documentation:** It serves as the single source of truth for the agent's memory.

## Inheritance
You can extend schemas.

```python
class BaseState(TypedDict):
    messages: List[str]

class RAGState(BaseState):
    documents: List[str]
```

## Quick Summary

**1-Line Recall:** **The State Schema is a TypedDict class that explicitly lists every field the graph tracks, serving as the API contract between nodes.**
