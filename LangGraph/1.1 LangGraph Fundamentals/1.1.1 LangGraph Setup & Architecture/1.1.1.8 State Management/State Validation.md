# State Validation

**Core Definition:** Ensuring that the data flowing through the graph meets required constraints.

## Runtime Validation with Pydantic
While `TypedDict` is mostly a compile-time hint, you can use Pydantic models as State.

```python
from pydantic import BaseModel, Field

class State(BaseModel):
    score: int = Field(ge=0, le=100) # Must be 0-100
```
If a node returns `{"score": 101}`, Pydantic raises a `ValidationError` immediately.

## Custom Validators
You can add `@field_validator` methods to your Pydantic state to enforce complex business rules (e.g., "End date must be after Start date").

## Guard Nodes
Alternatively, place a specific **Validation Node** after a generation step.
```python
def guard_node(state):
    if not is_valid(state["output"]):
        return {"error": "Invalid Output", "retry": True}
```

## Quick Summary

**1-Line Recall:** **Use Pydantic for strict, automatic schema enforcement at runtime, or use specific 'Guard Nodes' for logic-based validation.**
