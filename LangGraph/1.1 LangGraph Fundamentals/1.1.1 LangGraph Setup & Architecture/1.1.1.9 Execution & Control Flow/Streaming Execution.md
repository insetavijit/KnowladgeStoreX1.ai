# Streaming Execution

**Core Definition:** Receiving updates *while* the graph is running, rather than waiting for the end. Essential for chat UIs.

## 1. `graph.stream()`
Yields updates as each node finishes.

```python
for event in graph.stream(input_state):
    # event is usually a dict of {node_name: state_update}
    for node, update in event.items():
        print(f"Node {node} finished with: {update}")
```

## 2. Streaming Modes
You can control *what* is streamed via `stream_mode`.
-   `"values"`: Yields the full state after each step.
-   `"updates"` (Default): Yields only the changes (delta).
-   `"messages"`: Yields LLM tokens/messages specifically (useful for chatbots).

## 3. Streaming Tokens (LLM)
To get token-by-token output from an LLM node *through* the graph, you typically use `astream_events` (v2 API) or ensure your LLM is configured to stream and you consume the `"messages"` stream mode.

## Quick Summary

**1-Line Recall:** **Use `graph.stream()` to get incremental feedback; choose 'values' mode for full state snapshots or 'updates' mode for deltas.**
