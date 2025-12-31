# Typed vs Untyped State

**Core Definition:** Choosing between strict schema definitions (`TypedDict`) and loose dictionaries (`dict`).

## 1. Typed State (Recommended)
Using a class inheriting from `TypedDict`.
-   **Pros:** IDE support, catching typos (`sttae["mag"]` errors), clearer code.
-   **Cons:** Requires defining the structure upfront.
-   **Best For:** Production agents, teams.

```python
class State(TypedDict):
    count: int

def node(state: State):
    return {"count": state["count"] + 1}
```

## 2. Untyped State
Using a raw `dict` or `Any`.
-   **Pros:** Fast prototyping, highly dynamic workflows where keys aren't known.
-   **Cons:** No autocomplete, frequent `KeyError` bugs at runtime.
-   **Best For:** Quick experiments, 5-line scripts.

## The Middle Ground (Optional Fields)
If a field might not exist yet, use `Optional` or `NotRequired`.

```python
from typing import NotRequired

class State(TypedDict):
    required_key: str
    optional_key: NotRequired[str]
```

## Quick Summary

**1-Line Recall:** **Always prefer Typed State in production code to catch key-access errors at compile/lint time rather than crashing at runtime.**
