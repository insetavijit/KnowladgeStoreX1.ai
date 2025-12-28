# Return Value Patterns

**Core Definition:** The rules for what a node sends back to the graph to trigger state updates.

## 1. Partial Updates (The Standard)
You only return the keys you want to change. Keys you omit stay exactly the same.

```python
# State has {a: 1, b: 2}
def node(state):
    return {"a": 5}
# Result: {a: 5, b: 2}
```

## 2. Returning `None` (No-Op)
If a node runs but shouldn't change anything (e.g., a pure logging node), return an empty dict or None.

```python
def logger_node(state):
    print(state)
    return {} # No state change
```

## 3. The `Annotated` Effect
If a field in your state is annotated with `operator.add` (like `messages`), returning a value **appends** it rather than replacing it.

```python
# messages: Annotated[list, add]
def node(state):
    return {"messages": [params]} 
    # Appends [params], does NOT delete old history
```

## 4. Deleting Keys
To delete a key (if using a reducer that supports it), you often need a special sentinel value, but standard LangGraph TypedDicts don't support key deletion easily. Usually, you set it to `None` or an empty list.

## Quick Summary

**1-Line Recall:** **Return a dictionary of *changes*; omitted keys are preserved, and annotated keys (like lists) are merged/appended.**
