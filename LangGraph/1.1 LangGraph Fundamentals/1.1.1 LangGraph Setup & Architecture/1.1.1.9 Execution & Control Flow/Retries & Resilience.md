# Retries & Resilience

**Core Definition:** Automatically retrying nodes that fail due to transient issues (like network blips).

## Node-Level Retries
You can attach a `RetryPolicy` to any node during registration.

```python
from langgraph.prebuilt import RetryPolicy

workflow.add_node(
    "model_node", 
    call_model, 
    retry=RetryPolicy(
        max_attempts=3,
        initial_interval=1.0, # Wait 1s
        backoff_factor=2.0    # Then 2s, 4s
    )
)
```

## What is Retried?
-   **Exceptions:** Typically `Exception` (catch-all) or specific types if configured.
-   **Output:** If the node returns successfully, it is NOT retried.

## Running Policy
LangGraph uses a standard exponential backoff.
-   *Warning:* If a node has side effects (like sending an email) and fails *after* the email is sent but *before* returning, a retry might send the email again. Make nodes idempotent!

## Quick Summary

**1-Line Recall:** **Configure `RetryPolicy` on nodes to handle flakey APIs automatically; ensure your nodes are idempotent to safely handle re-execution.**
