# Explicit Error Handling

## 1. Core Definition
**Explicit Error Handling** in LangGraph means modeling failures as valid branches in the graph rather than letting exceptions crash the Python process. Since agents interact with unreliable external tools and stochastic models, errors are *expected* behavior, not exceptional.

## 2. Key Technical Details
*   **Try/Except Blocks**: Wrap vulnerable code (API calls) in try/except blocks *inside* the node.
*   **Error Flags**: On exception, return a state update like `{"error": "Timeout", "status": "failed"}` instead of raising.
*   **Conditional Routing**: Use a `route_submission` function that checks `if state.get("error"): return "retry_node"`.
*   **Fallbacks**: Implement nodes solely for recovery (e.g., "Use Simple Search" if "Advanced Search" fails, or "Apologize to User" if all else fails).

## 3. Mental Model
*   **Visual**: A detour sign on a roadmap. The main road is blocked (Error), but the map explicitly shows a secondary route to get back on track. It doesn't just end in a cliff.
*   **Analogy**: A spare tire. Cars are designed with the knowledge that tires go flat. The procedure (pull over, change tire) is defined. You don't abandon the car on the highway.

## 4. Code Example (The 'Error' Edge)
```python
def tool_node(state):
    try:
        result = unsafe_api_call()
        return {"result": result, "error": None}
    except Exception as e:
        # Capture error in state
        return {"error": str(e)}

def router(state):
    if state["error"]:
        return "error_handler" # Explicit recovery path
    return "next_step"

workflow.add_conditional_edges("tool_node", router, ...)
```

## 5. One-Line Recall
Treat errors as data (state updates) and route them to recovery nodes; never let an unhandled exception kill a long-running graph.
