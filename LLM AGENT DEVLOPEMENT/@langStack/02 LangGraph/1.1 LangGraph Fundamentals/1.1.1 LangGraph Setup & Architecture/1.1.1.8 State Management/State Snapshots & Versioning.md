# State Snapshots & Versioning

**Core Definition:** The ability to save the state at every step, creating a "Time Machine" for your agent.

## Implicit Versioning
LangGraph Checkpointers (like `MemorySaver`) automatically version the state.
-   Step 1: Version 1
-   Step 2: Version 2

## Inspecting History
You can query the graph history to see *exactly* what the state was 5 turns ago.
```python
history = list(graph.get_state_history(config))
for snapshot in history:
    print(snapshot.values)
```

## Replay (Time Travel)
You can resume execution from ANY snapshot.
1.  Find a checkpoint config (`thread_id`, `checkpoint_id`).
2.  Run `graph.invoke(..., config=subset_config)`.
3.  The graph rewinds logic to that point and continues.

## Quick Summary

**1-Line Recall:** **Checkpointers automatically version state at every step, enabling powerful debugging, replayability, and 'human-in-the-loop' editing.**
