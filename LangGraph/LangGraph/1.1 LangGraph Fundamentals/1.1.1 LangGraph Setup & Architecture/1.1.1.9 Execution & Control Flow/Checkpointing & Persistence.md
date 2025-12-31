# Checkpointing & Persistence

**Core Definition:** The ability to save the state of the graph to a database after every step, allowing for pause, resume, and rollback.

## The Checkpointer Interface
You must pass a `checkpointer` when compiling.

```python
from langgraph.checkpoint.memory import MemorySaver

checkpointer = MemorySaver() # In-memory (not persistent across restarts)
graph = workflow.compile(checkpointer=checkpointer)
```

## Persistent Backends
For production, use a real backend.
-   `AsyncSqliteSaver`
-   `PostgresSaver`
-   `RedisSaver` (Community)

## Config Usage
To read/write from the checkpointer, you MUST provide a `thread_id` in the config at runtime.

```python
config = {"configurable": {"thread_id": "session_1"}}
graph.invoke(inputs, config=config)
```

## How it Works
1.  Graph starts step.
2.  Step finishes.
3.  Graph serializes state.
4.  Graph writes state to DB with `thread_id` and `checkpoint_id`.
5.  Graph proceeds to next step.

## Quick Summary

**1-Line Recall:** **Checkpointers save state to a DB after every node execution using a 'thread_id'; this is strictly required for 'Human-in-the-loop' features.**
