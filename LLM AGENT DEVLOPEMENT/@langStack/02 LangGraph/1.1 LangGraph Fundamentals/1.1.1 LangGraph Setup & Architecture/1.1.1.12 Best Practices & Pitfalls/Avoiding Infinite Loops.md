# Avoiding Infinite Loops

## 1. Core Definition
**Avoiding Infinite Loops** is a critical safety practice in cyclic graphs. An agent might get stuck in a "Plan -> Critique -> Plan -> Critique" loop where the critique is never satisfied. Without safeguards, this burns indefinite money (API costs) and hangs the user request.

## 2. Key Technical Details
*   **Recursion Limit**: LangGraph sets a default `recursion_limit=25` on `app.invoke`. Always set this to a reasonable value for your use case.
*   **Cycle Counters**: Maintain an explicit counter in your state (e.g., `iteration_count: int`). Increment it on every loop.
*   **Conditional Exit**: In your routing logic, check `if iteration_count > MAX_RETRIES: return END`.
*   **Progress Detection**: More advanced guards check if the state is actually changing/improving. If the agent generates the exact same plan twice, force an exit.

## 3. Mental Model
*   **Visual**: A "Time To Live" (TTL) hop counter on a network packet. If the counter hits 0, the packet is dropped, preventing it from circling the internet forever.
*   **Analogy**: A parent telling a child "You can try 3 times to unlock the door, then I'll do it." (Hard limit on attempts).

## 4. Code Example (Iteration Cap)
```python
# 1. State Schema
class State(TypedDict):
    retries: int
    ...

# 2. Increment in Node
def generator(state):
    return {"retries": state["retries"] + 1, ...}

# 3. Router logic
def should_continue(state):
    if state["retries"] >= 3:
        return END # Force stop
    return "critique"
```

## 5. One-Line Recall
Always guard loops with a maximum iteration count to prevent runaway costs and hung processes.
