# Decision & Routing Nodes

**Core Definition:** Logic that determines "Where to go next?"

## 1. Conditional Edges (Route by Logic)
Often, the routing logic doesn't need to update the state, so it sits in a **Conditional Edge**, not a Node.

```python
def should_continue(state):
    if state["messages"][-1].tool_calls:
        return "tools"
    return END

workflow.add_conditional_edges("agent", should_continue)
```

## 2. Decision Nodes (Route by Thinking)
Sometimes the decision is complex and requires an LLM call. Specifically, a "Classifier" or "Router" node.

```python
# This node actually modifies state with the decision
def classifier_node(state):
    response = model.invoke("Is this about Support or Sales?")
    category = parse(response)
    return {"category": category}

# The edge just reads the category
def route_category(state):
    return state["category"] # "support" or "sales"
```

## 3. Determinism
-   **Edges** should ideally be fast and deterministic (pure logic).
-   **Nodes** handle the probabilistic/slow part (LLM thinking).

## Quick Summary

**1-Line Recall:** **Use Conditional Edges for pure logic; use Decision Nodes (Classifiers) when you need the LLM to *decide* where to go.**
