# State Immutability

## 1. Core Definition
**State Immutability** is a functional programming principle applied to graph execution. While Python's dictionaries are mutable, good practice in LangGraph is to treat the *input state* to a node as read-only and return a *new* partial dictionary for the update. Directly mutating `state["messages"]` inside a node can lead to confusing bugs, especially with parallel branches or complex reducers.

## 2. Key Technical Details
*   **Copy-on-Write**: Conceptually, LangGraph creates a new state version after every step.
*   **Reducers**: LangGraph relies on "reducer" functions (like `operator.add` for lists) to merge updates. If you mutate the list in place *and* return it, you might accidentally double-append data depending on the implementation details.
*   **Debugging**: Immutable history allows "Time Travel" debugging. If you mutate state in place, you overwrite the history, making it impossible to see what the state was 3 steps ago.

## 3. Mental Model
*   **Visual**: A chain of snapshots. V1 is a photo. V2 is a photo of V1 + changes. You never "draw on" the original V1 photo.
*   **Analogy**: Accounting Ledger. You never erase a line in a ledger to change a balance. You add a *new* line (transaction) that updates the balance. This ensures a perfect audit trail.

## 4. Code Example (Mutation vs Update)
```python
# BAD (In-place mutation)
def bad_node(state):
    state["count"] += 1 # Side effect on input object
    state["messages"].append("New msg") 
    return state # Confusing for reducer

# GOOD (Functional Update)
def good_node(state):
    # Return ONLY the delta/change
    return {
        "count": state["count"] + 1,
        "messages": ["New msg"] # Reducer will handle the append
    }
```

## 5. One-Line Recall
Return *updates* (deltas), don't mutate the input state directly; this ensures predictable merging and clean history tracking.
