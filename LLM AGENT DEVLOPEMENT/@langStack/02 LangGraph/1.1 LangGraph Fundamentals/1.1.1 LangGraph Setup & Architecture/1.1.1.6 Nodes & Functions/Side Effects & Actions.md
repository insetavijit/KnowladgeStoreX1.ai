# Side Effects & Actions

**Core Definition:** Actions that impact the world outside the graph (logging, API calls, DB writes, sending emails).

## The Principle of Isolation
Keep "Thinking" separate from "Acting" if possible.
-   **Pure Nodes:** Determinstic, just data processing.
-   **Effect Nodes:** Do the dirty work.

## Implementing Side Effects

### 1. Logging
Use the `logging` module. This is a "read-only" side effect.

```python
def log_step(state):
    logger.info(f"Step completed: {state['status']}")
    return {}
```

### 2. External APIs (Write)
When sending an email or charging a card:
-   **Wrap in try/except.**
-   **Return status to state.**

```python
def send_email_node(state):
    try:
        api.send(state["email_draft"])
        return {"email_status": "sent"}
    except Exception as e:
        return {"email_status": "failed", "error": str(e)}
```

## Idempotency Warning
If your graph gets interrupted and you rerun it, **nodes might run again**.
-   *Dangerous:* Charging a credit card.
-   *Protection:* Check if the action was already done *before* doing it.
    ```python
    if state.get("payment_processed"):
        return {} # Skip
    ```

## Quick Summary

**1-Line Recall:** **Handle side effects carefully; assume nodes might be re-executed, so implement checks to prevent double-charging or duplicate actions.**
