# Field-Level Updates

**Core Definition:** The ability to modify one specific key in the state without having to read/write the entire object.

## The Pattern
LangGraph nodes return *partial* dicts.

```python
# State has 50 fields
def update_score_node(state):
    # I only care about 'score'
    return {"score": 100} 
    # The other 49 fields remain untouched.
```

## Why this matters
In traditional state management (like Redux), you often have to spread the old state: `return { ...state, score: 100 }`.
In LangGraph, **You do NOT need to spread**. The graph engine merges your return value into the global state.

## Nulling out fields
If you want to *clear* a field, your node must explicitly return a value that represents "empty" (like `None` or `[]`), provided your schema allows it.
*Note: Some custom reducers might interpret `None` as "no update", so checking definitions is key.*

## Quick Summary

**1-Line Recall:** **Nodes behave like 'Diff Generators'; they output only what needs to change, and the graph engine handles the merging.**
