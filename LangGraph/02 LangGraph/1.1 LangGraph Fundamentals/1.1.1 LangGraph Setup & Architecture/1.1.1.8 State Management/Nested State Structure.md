# Nested State Structure

**Core Definition:** Organizing complex agents by grouping related fields into sub-objects (nested TypedDicts or Pydantic models).

## The "Flat vs Nested" Debate
-   **Flat:** `user_name`, `user_age`, `bot_mood`. Easy to access.
-   **Nested:** `user: {name, age}`, `bot: {mood}`. structured.

## Updating Nested State
LangGraph's default merge is **Shallow**.
If you update `user`, you overwrite the *whole* user object unless you define a custom deep-merge reducer.

### The Shallow Replacement Problem
```python
# Old State: user = {name="A", age=10}
# Node returns: {"user": {"age": 11}}
# New State: user = {"age": 11}  <-- NAME IS LOST!
```

## Best Practice
Either:
1.  Keep state relatively flat.
2.  Or always read the full nested object, modify it, and return the full object.
3.  Or use Pydantic models with custom update logic.

## Quick Summary

**1-Line Recall:** **Nested state organizes data but beware of default 'Shallow Merge' behavior; partial updates to nested dicts often overwrite missing keys.**
