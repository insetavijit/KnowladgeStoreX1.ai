# Callbacks & Monitoring

**Core Definition:** **Callbacks** are the event listeners of the LangChain ecosystem. They allow you to "hook into" the execution of your agent to see what's happening (logging), stream tokens to the UI (streaming), or track costs (monitoring).

**Role in LangGraph:** Because LangGraph nodes run standard LangChain Runnables, the entire callback system works out-of-the-box.

## Key Concepts

### 1. Events
The lifecycle hooks you can listen to:
-   `on_chain_start`: When a node or chain begins.
-   `on_llm_start`: Before the prompt hits the API.
-   **`on_llm_new_token`**: The bread and butter of streaming UIs; fires for every generated chunk.
-   `on_tool_start` / `on_tool_end`: Tracking tool usage.
-   `on_chain_error`: When things break.

### 2. LangSmith (Tracing)
The official observability platform.
-   **How it works:** You set `LANGCHAIN_TRACING_V2=true` in your environment.
-   **What you see:** A waterfall visualization of every step in your graph.
-   **Why it's vital for Graphs:** Graphs are complex. "Why did the agent loop 10 times?" LangSmith shows you the exact outputs that caused the loop.

### 3. Custom Callbacks
You can write your own handlers.
```python
class MyLogger(BaseCallbackHandler):
    def on_llm_new_token(self, token, **kwargs):
        print(token, end="") # Poor man's streaming
```

### 4. Passing Callbacks
You pass callbacks at runtime via the `config` object in LangGraph/Runnables.
```python
graph.invoke(inputs, config={"callbacks": [MyLogger()]})
```

## Monitoring Costs

Callbacks are also where token usage is aggregated.
-   **`get_openai_callback()`** (Legacy context manager) tracks total tokens and cost for a run.
-   **LangSmith** automatically tracks costs per project/run.

## Quick Summary

**1-Line Recall:** **Callbacks give you X-ray vision into the agent's execution; they are the mechanism for Streaming and Tracing (LangSmith).**
