# Interrupts & Human-in-the-Loop

**Core Definition:** Pausing graph execution to wait for external input/approval.

## 1. Interrupt Before/After
You can configure the graph to *always* stop before entering a node.

```python
graph = workflow.compile(interrupt_before=["human_review"])
```

## 2. The Flow
1.  Graph runs.
2.  Graph hits "human_review".
3.  Graph **Suspends** execution and saves state (Checkpointing REQUIRED).
4.  `invoke()` returns.

## 3. Resuming
The human (via UI) looks at the state, maybe modifies it.
Then you call `invoke(None, config)` with the *same* thread ID.
-   The graph sees it was paused at "human_review".
-   It resumes execution from there.

## 4. `interrupt()` Function (Dynamic)
Inside a node, you can call `interrupt("Give me input")`.
-   The graph pauses.
-   When resumed, the return value of `interrupt()` becomes the input provided by the user during resume.

## Quick Summary

**1-Line Recall:** **Use `interrupt_before` limits to pause the graph at specific nodes, requiring a subsequent `invoke` call to resume; efficient for approval workflows.**
