# Validating the Setup

**Core definition:** Determining if your environment is ready for development by running a minimal "Hello World" graph.

**Position in ecosystem:**
The final check before starting real work.

**Key idea:**
- **Version Check:** `print(langgraph.__version__)`.
- **Smoke Test:** Compile a trivial graph (Start -> End).

## The "Smoke Test" Script

```python
from langgraph.graph import StateGraph, START, END
from typing import TypedDict

class State(TypedDict):
    pass

def node(state):
    print("Graph is working!")
    return state

builder = StateGraph(State)
builder.add_node("test", node)
builder.add_edge(START, "test")
builder.add_edge(test, END)

app = builder.compile()
app.invoke({})
```

If this prints "Graph is working!", you are clear for takeoff.

## Quick Summaries

**30-second version:** Turn the hey key. Does the engine start? Good. You don't need to drive to the grocery store to know the car is working; just listening to the engine hum (running the smoke test) is enough.

**One-line recall:**
**Run a minimal 2-node graph to confirm end-to-end functionality.**

---

## Linked Concepts
- [[Installing LangGraph]]
- [[Troubleshooting Installation Issues]]
- [[Testing Environment]]

---
**Last updated:** December 2025
