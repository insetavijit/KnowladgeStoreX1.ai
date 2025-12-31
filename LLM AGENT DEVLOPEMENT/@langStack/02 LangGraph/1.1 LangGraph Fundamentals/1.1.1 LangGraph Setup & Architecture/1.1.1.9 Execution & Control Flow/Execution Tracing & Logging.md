# Execution Tracing & Logging

**Core Definition:** Recording the step-by-step execution details for audit and debugging.

## LangSmith Integration
LangGraph is built by LangChain, so it integrates natively with **LangSmith**.
-   Set `LANGCHAIN_TRACING_V2=true` env var.
-   Run your graph.
-   View full traces (inputs, outputs, latency, tokens) in the LangSmith UI.

## Local Logging
You can simply print inside nodes, but it gets messy in async.
Better to rely on the stream events.

```python
for event in graph.stream(inputs):
    # Logs "Node X starting", "Node X finished"
    pass
```

## Quick Summary

**1-Line Recall:** **Enable LangSmith tracing for best-in-class debugging; alternatively, analyze the `graph.stream()` events to log execution flow.**
