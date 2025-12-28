# Memory & Graph State

**Core Definition:** State is the "Blood" of the graph. It flows through the veins (Edges) and powers the organs (Nodes).

**The Paradigm Shift:**
-   **Old Way (Chains):** Data flowed as arguments `func(input) -> output`.
-   **New Way (Graph):** Data resides in a central, shared object (`GraphState`). Nodes just modify this object.

## 1. The Shared State
Defined as a `TypedDict`.
```python
class State(TypedDict):
    input: str
    output: str
    steps: List[str]
```

## 2. State Updates (Reducers)
When a node returns `{"output": "Hello"}`, it **merges** into the state. It does NOT replace the whole state.
-   **Default:** Overwrite (Last write wins).
-   **Annotated:** Append (Add to list).
    ```python
    steps: Annotated[List[str], operator.add]
    ```

## 3. Threading
When using a **Checkpointer** (Persistence), LangGraph creates a "Thread" ID.
-   `config={"configurable": {"thread_id": "1"}}`
-   The State is saved to a database keyed by this Thread ID.
-   This allows you to resume a graph days later.

## 4. Immutable vs Mutable
Under the hood, LangGraph creates a *new version* of the state at every step (Immutable principles).
-   This enables "Time Travel" (rewinding the debugger).
-   You never "mutate" the state object in place; you return a *diff*.

## Quick Summary

**1-Line Recall:** **Nodes don't pass data directly to each other; they read from and write to a shared, persistent State object.**
