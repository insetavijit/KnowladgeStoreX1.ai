# Memory & Persistence

**Core definition:** **Persistence** is the ability to save the state of a graph to a durable storage (database) so workflows can span seconds, days, or weeks. **Memory** is the ability to recall past interactions in future runs.

**Position in ecosystem:**
Without persistence, if your script stops, the agent loses its brain. With persistence, agents are "immortal" until completed.

**Key idea:**
- **Checkpointers:** Objects that save the `State` at every step.
- **Thread ID:** A unique key to look up a specific conversation history.

## Essential Characteristics

**1. Resume Capability:** Continue a conversation exactly where it left off.
**2. Time Travel:** Load a previous checkpoint and branch off a new path (multiverse).
**3. Backends:** In-memory (testing), SQLite (local), Postgres (production).
**4. Async/Long-running:** Essential for waiting on human input which might take days.

## Code Gist

```python
from langgraph.checkpoint.sqlite import SqliteSaver

memory = SqliteSaver.from_conn_string(":memory:")

# pass checkpointer to compile
graph = workflow.compile(checkpointer=memory)

# invoke with a specific thread
config = {"configurable": {"thread_id": "123"}}
graph.invoke(inputs, config)
```

## Quick Summaries

**30-second version:** It's a "Save Game" feature. Without it, you start from Level 1 every time you talk to the agent. With it, the agent remembers you defeated the boss yesterday and specific details about your inventory.

**One-line recall:**
**Persistence allows graphs to pause, resume, and remember across sessions.**

---

## Linked Concepts
- [[State Management]]
- [[Human-in-the-Loop]]
- [[Performance & Cost]]

---
**Last updated:** December 2025
