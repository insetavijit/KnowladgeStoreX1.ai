# State Access Patterns

**Core Definition:** How to read data from the `state` object within a node efficiently and safely.

## 1. Full State Access
Simply access keys like a dictionary.

```python
def my_node(state):
    # Read
    history = state["messages"]
    user = state["user_profile"]
    
    # Logic...
```

## 2. Unpacking (Destructuring)
For cleaner code, unpack commonly used fields at the start.

```python
def my_node(state):
    messages, count = state["messages"], state["retry_count"]
```

## 3. Read-Only Safety
Remember: **State is Immutable-ish.**
You cannot do `state["messages"].append(msg)`.
This creates a local modification but **Does NOT update the graph**.
You *must* return the update: `return {"messages": [msg]}`.

## 4. Derived State
Sometimes you need to calculate something based on state.
-   *Bad:* Calculating it inside every node.
-   *Good:* Write a helper function.

```python
def get_last_human_message(state):
    for m in reversed(state["messages"]):
        if isinstance(m, HumanMessage):
             return m
    return None
```

## Quick Summary

**1-Line Recall:** **Treat `state` as read-only input; local mutations are lost unless returned explicitly as a dict update.**
