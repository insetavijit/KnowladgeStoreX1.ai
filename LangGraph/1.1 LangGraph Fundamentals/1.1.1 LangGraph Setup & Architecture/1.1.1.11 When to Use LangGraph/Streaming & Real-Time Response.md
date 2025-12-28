# Streaming & Real-Time Response

## 1. Core Definition
**Streaming** is the capability to emit intermediate output to the user *while* the graph is still executing. In complex agentic systems that might take 30+ seconds to complete a task, streaming is essential for User Experience (UX) to show liveness (e.g., showing "Designing plan...", "Calling Google Search...", "Reading results...").

## 2. Key Technical Details
*   **Streaming Modes**: LangGraph supports multiple streaming modes:
    *   `updates`: Emits the state update after each node completes.
    *   `messages`: Emits partial tokens from LLM calls (token-by-token streaming).
    *   `events`: Emits custom events or debug data.
*   **Perception of Speed**: Even if the total time is the same, showing the status of each node ("Thinking...", "Browsing...") makes the system feel faster and more responsive.
*   **UI Integration**: Modern AI UIs (like ChatGPT) rely on streaming. LangGraph provides the backend infrastructure to stream the *structural* progress (graph events) alongside the *content* progress (tokens).

## 3. Mental Model
*   **Visual**: A progress bar with text updates. `[..Node A done..] [..Node B working..] [..Token..Token..]`.
*   **Analogy**: Watching a pizza delivery tracker. You see "Order Received," "Baking," "Out for Delivery." You don't get the pizza instantly, but knowing where it is in the process reduces anxiety and makes the wait tolerable.

## 4. Code Example (Streaming)
```python
# Client side code pattern
async for event in agent_app.stream_events(inputs, version="v1"):
    kind = event["event"]
    
    if kind == "on_chat_model_stream":
        # Stream the actual text tokens
        print(event["data"]["chunk"].content, end="")
        
    elif kind == "on_tool_start":
        # Show tool usage in UI
        print(f"\n[Using Tool: {event['name']}]")
```

## 5. One-Line Recall
Use LangGraph when you need to provide real-time visibility (tokens or node updates) into a multi-step execution flow.
