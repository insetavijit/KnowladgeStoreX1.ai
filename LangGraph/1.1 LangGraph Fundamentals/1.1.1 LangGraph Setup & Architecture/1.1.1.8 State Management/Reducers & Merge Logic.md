# Reducers & Merge Logic

**Core Definition:** Functions that define *how* a new value from a node is combined with the existing value in the state.

## Default Behavior: Replacement
If you don't specify a reducer, the new value overwrites the old one.

## Custom Reducers
A reducer is just a function `f(old, new) -> resulting`.

```python
def add_scores(old: int, new: int) -> int:
    return old + new

class State(TypedDict):
    score: Annotated[int, add_scores]
```

## Built-In Reducers
LangGraph (via `langgraph.graph.message`) provides `add_messages`.
You can also use `operator.add` for simple lists.

```python
import operator
from typing import Annotated

class State(TypedDict):
    items: Annotated[list, operator.add]
```
*Note: `operator.add` concatenates lists. `[1] + [2] = [1, 2]`.*

## Handling "Last Write Wins"
This is the default for normal types, but you can be explicit if you want to emphasize it.

## Quick Summary

**1-Line Recall:** **Reducers solve the conflict of 'Old Value vs New Value'; essentially `state[key] = reducer(state[key], update[key])`.**
