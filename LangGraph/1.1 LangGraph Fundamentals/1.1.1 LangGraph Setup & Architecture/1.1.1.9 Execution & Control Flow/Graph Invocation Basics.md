# Graph Invocation Basics

**Core Definition:** The process of running your compiled graph from Start to Finish (or interruption).

## The Prerequisite: Compilation
You cannot run a `StateGraph` object directly. You must compile it first.
```python
graph = workflow.compile()
```
This returns a `CompiledGraph` runable.

## The Standard Invoke
This runs the graph synchronously. It blocks your Python thread until the graph hits `END`.

```python
final_state = graph.invoke(
    {"messages": [HumanMessage(content="Hi")]},
    config={"configurable": {"thread_id": "1"}}
)
```

## Input vs Output
-   **Input:** Can be a partial dictionary (only the keys you want to set).
-   **Output:** Is usually the *entire* state dictionary after the last node runs.

## Waiting Behavior
`invoke()` waits for:
1.  All nodes to finish.
2.  Or a `RecursionLimitError`.
3.  Or an `Interrupt`.

## Quick Summary

**1-Line Recall:** **`graph.invoke(input)` is the standard synchronous entry point; it blocks until execution completes and returns the final state.**
