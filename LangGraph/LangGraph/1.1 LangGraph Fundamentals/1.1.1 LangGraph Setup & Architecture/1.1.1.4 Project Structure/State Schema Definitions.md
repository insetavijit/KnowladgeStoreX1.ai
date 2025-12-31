# State Schema Definitions

**Core Definition:** Centralizing the definition of your `GraphState` (the shared memory dict) in a dedicated module.

**Why?**
The State is the contract between all your nodes. If you define it inside `graph.py` and also need it in `nodes/utils.py`, you'll get circular imports.

## Best Practice: `src/state.py`

Create a standalone file that only contains data structures.

```python
# src/state.py
from typing import TypedDict, Annotated, List, Union
from langchain_core.messages import BaseMessage
import operator

class AgentState(TypedDict):
    # The conversation history
    messages: Annotated[List[BaseMessage], operator.add]
    # Internal variables
    user_id: str
    retry_count: int
    context: List[str]
```

## TypedDict vs Dataclass

-   **TypedDict:** Recommended by LangGraph. It behaves like a dictionary at runtime (compatible with JSON) but gives you type checking during development.
-   **Pydantic:** Can be used, but LangGraph's native state handling is optimized for TypedDict.

## Avoiding Circular Imports

**Dependency Graph:**
`Nodes` depend on `State`.
`Graph` depends on `Nodes` AND `State`.

If `State` imports `Nodes`, you break the cycle. **Keep `state.py` clean.**

## Quick Summary

**1-Line Recall:** **Define your `AgentState` in a dedicated `src/state.py` file to prevent circular imports and provide a single source of truth.**
