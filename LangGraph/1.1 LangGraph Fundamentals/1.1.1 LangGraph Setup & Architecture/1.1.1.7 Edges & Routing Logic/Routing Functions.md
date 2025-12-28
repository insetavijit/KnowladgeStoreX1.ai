# Routing Functions

**Core Definition:** The actual Python logic inside a conditional edge that makes the decision.

## Properties of a Good Router

1.  **Pure Function:** Ideally, it should just read state and return a string. It should NOT call APIs (put that in a Node).
2.  **Fast:** Since it runs between nodes, slow routers add latency.
3.  **Complete:** It should handle ALL possible cases.

## Assessing State
You can route based on:

### 1. Message Content (Most Common)
Did the LLM output text or a tool call?
```python
def route_tools(state):
    msg = state["messages"][-1]
    if msg.tool_calls:
        return "tools"
    return END
```

### 2. Structured Output (Classifiers)
Did the LLM classify this as "Billing" or "Support"?
```python
def route_category(state):
    return state["category"] # "billing" or "support"
```

### 3. Context Variables
Is this the 5th retry?
```python
def limit_retries(state):
    if state["retry_count"] > 3:
        return END
    return "retry_node"
```

## Naming the Router
When visualizing, this function's name appears on the Diamond node. Name it well: `should_continue`, `check_safety`, `route_by_topic`.

## Quick Summary

**1-Line Recall:** **Routing Functions are the "If statements" of your graph; keep them fast, pure, and ensure they cover all possible return paths.**
