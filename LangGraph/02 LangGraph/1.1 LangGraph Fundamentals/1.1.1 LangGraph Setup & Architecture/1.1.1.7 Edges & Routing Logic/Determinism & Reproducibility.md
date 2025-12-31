# Determinism & Reproducibility

**Core Definition:** Ensuring that for a given input, the graph takes the exact same path every time.

## Why it Matters
Debugging an agent is impossible if the path changes randomly.

## Sources of Non-Determinism
1.  **LLM Temperature:** Use `temperature=0` for logic/routing nodes.
2.  **Set Iteration:** In Python, `for x in set_of_nodes` has random order. Always sort calls.
3.  **Race Conditions:** In Fan-In, if reducer is order-dependent.

## Enforcing Determinism in Routers
Bad:
```python
if random.random() > 0.5: return "A"
```

Good:
```python
# Hash the input string to decide
if hash(state["input"]) % 2 == 0: return "A"
```

## Testing for Determinism
LangGraph allows "Time Travel" (replaying from a checkpoint).
-   If you replay a step, the *Router* logic runs again.
-   It **MUST** return the same node as before, otherwise the history becomes invalid.

## Quick Summary

**1-Line Recall:** **Routing logic must be deterministic; avoid randomness or external side-effects (like Checking Time) inside a router function.**
