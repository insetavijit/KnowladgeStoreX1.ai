# Error Handling & Recovery

**Core definition:** **Error Handling** ensures that when a node fails (e.g., API timeout), the graph doesn't crash but instead **routes** to a recovery path or **retries** the action.

**Position in ecosystem:**
Essential for production-grade agents. LLMs and network calls are flaky; your graph structure must be robust.

**Key idea:**
- **Node-level Try/Catch:** Handle exceptions within the Python function.
- **Graph-level Fallbacks:** If Node A fails, edge routing sends flow to Node B (Recovery).
- **Retries:** Configurable retry policies for flaky external services.

## Essential Characteristics

**1. Resilience:** The agent can survive bad inputs or temporary outages.
**2. Self-Correction:** The agent can see an error message and try a different approach (e.g., "Tool arguments invalid," so the agent rewrites the arguments).
**3. Dead-end Avoidance:** ensuring the graph always reaches an `END` state eventually.

## Common Patterns

### The "Fallback" Pattern
1.  Attempt **Primary Tool**.
2.  If Success -> Continue.
3.  If Error -> Route to **Fallback Tool** (or ask Human).

### The "Retry" Pattern
Automatic retries with exponential backoff for network errors.

## Code Gist

```python
# Retry configuration
def my_node(state):
    # implementation ...
    pass

# When compiling, add retry policy
app = workflow.compile()
# (Note: Specific retry logic is often handled inside node functions or via LangSmith config)
```

## Quick Summaries

**30-second version:** If you trip while walking, you don't just lay there forever. You get up and brush yourself off. Error handling gives the agent the ability to stand back up, or at least call for help, instead of crashing the entire program.

**One-line recall:**
**Error handling turns crashes into decision points.**

---

## Linked Concepts
- [[Control Flow & Routing]]
- [[Human-in-the-Loop]]
- [[Testing & Debugging]]

---
**Last updated:** December 2025
