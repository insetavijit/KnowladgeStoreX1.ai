# State Updates

**Core Definition:** The mechanism by which a node changes the global graph state.

## The Update Contract
A node returns a value (usually a `dict`). LangGraph takes this value and **Applies** it to the current state based on the schema's "Reducers".

## 1. Overwrite (Default)
For standard types (`int`, `str`, `dict`), the new value replaces the old value.
-   Old: `{"status": "pending"}`
-   Node Returns: `{"status": "done"}`
-   New: `{"status": "done"}`

## 2. Append (Annotated)
For lists annotated with `operator.add`, the new value is appended.
-   Old: `{"messages": ["A"]}`
-   Node Returns: `{"messages": ["B"]}`
-   New: `{"messages": ["A", "B"]}`

## 3. No Change
If a key is omitted from the return dict, it retains its old value.

## 4. Deletion
Deleting a key usually requires a custom reducer or setting it to a specific sentinel value (e.g., `None`), depending on your specific reducer logic.

## Quick Summary

**1-Line Recall:** **State updates are merges, not full replacements; specific behavior (overwrite vs append) is defined by the annotations in the State Schema.**
