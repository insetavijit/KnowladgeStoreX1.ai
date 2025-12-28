# State Management

**Core definition:** **State Management** in LangGraph refers to the **schema and storage** of data that persists and evolves as the graph executes. It is the "memory" of the agent.

**Position in ecosystem:**
In standard scripts, variables are ephemeral. In LangGraph, `State` is a first-class citizen that every node receives and can modify.

**Key idea:**
- **State Schema:** Defines the structure of data (e.g., `messages`, `user_id`).
- **Reducers:** Logic for *how* updates are merged (e.g., append to list vs. overwrite).

## Essential Characteristics

**1. TypedSchema:** Typically defined using `TypedDict` or Pydantic models for type safety.
**2. Shared Context:** All nodes access the same state object.
**3. Append vs. Overwrite:** You control if a node's output *replaces* a key or *adds* to it (critical for chat history).
**4. Persistence:** State can be saved to databases (checkpointers) to resume sessions later.

## Schema Example (Python)

```python
from typing import TypedDict, Annotated
import operator

class AgentState(TypedDict):
    # 'messages' key will APPEND new items instead of overwriting because of operator.add
    messages: Annotated[list[str], operator.add]
    # 'current_step' will OVERWRITE the previous value
    current_step: str
```

## How It Works

1.  **Input:** Graph starts with an initial state.
2.  **Node Execution:** Node A runs, takes `state`, returns `{'current_step': 'research'}`.
3.  **State Update:** The graph framework updates the global state with the changes.
4.  **Next Node:** Node B receives the *new* state.

## Common Pitfalls

- **Mutable Defaults:** Not initializing lists correctly.
- **Infinite Growth:** Forgetting to trim long message histories (context window limits).
- **Race Conditions:** In complex async graphs (though LangGraph handles most sequential locking).

## Quick Summaries

**30-second version:** The State is the "clipboard" passed between every person (node) in the room. Some people erase the clipboard and write new text (overwrite), while others just add sticky notes to the bottom (append/reduce). This ensures everyone knows what has happened so far.

**One-line recall:**
**State is the shared, evolving memory of the graph run.**

---

## Linked Concepts
- [[Introduction to State]]
- [[Memory & Persistence]]
- [[Nodes & Edges]]

---
**Last updated:** December 2025
