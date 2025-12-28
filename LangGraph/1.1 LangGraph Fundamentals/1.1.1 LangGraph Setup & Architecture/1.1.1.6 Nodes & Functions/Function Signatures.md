# Function Signatures

**Core Definition:** The input arguments and return types required for a function to be a valid LangGraph node.

## Standard Signature
The most common signature is:

```python
from typing import Dict, Any

def node_name(state: StateType) -> Dict[str, Any]:
    ...
```

1.  **Input:** The `state` argument receives the *current snapshot* of the graph state.
2.  **Output:** A dictionary representing *updates*. Keys must match fields in your `State` schema.

## Advanced Signatures

### 1. Injected Configuration
You can optionally accept a `config` argument to access runtime parameters (like `thread_id` or `user_id`).

```python
from langchain_core.runnables import RunnableConfig

def node_name(state: StateType, config: RunnableConfig):
    user_id = config.get("configurable", {}).get("user_id")
    ...
```

### 2. Returning `Command` (New in v0.2)
Instead of returning a dict, you can return a `Command` object to dynamically update state *and* direct control flow (goto) in one step.

```python
from langgraph.types import Command

def node_name(state):
    return Command(
        update={"messages": [...]},
        goto="next_node"
    )
```

## Compilation Errors
If your node modifies a key that isn't in the `State` TypedDict, LangGraph won't error *until runtime* (usually), but your IDE type checker should catch it if you use proper type hints.

## Quick Summary

**1-Line Recall:** **Nodes accept `(state)` or `(state, config)` and typically return a dictionary of state updates.**
