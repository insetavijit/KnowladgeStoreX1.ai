# Conditional Starts & Ends

**Core Definition:** While a graph *must* have a global `START` and `END`, how you enter and leave can be dynamic.

## Conditional END (Early Exit)
You don't have to wait for the whole chain to finish.

```python
def check_relevance(state):
    if state["is_irrelevant"]:
        return END # Exit immediately
    return "generate"
```
**Use Case:** Safety filters. If the user input is unsafe, exit before calling the expensive LLM.

## Conditional START (Entrypoint Routing)
You can define `START` to be a conditional router immediately.

```python
workflow.set_conditional_entry_point(
    route_by_user_type,
    {
        "premium": "gpt4_node",
        "free": "gpt3_node"
    }
)
```
**Use Case:** A/B Testing or User Tiering. The very first thing the graph does is decide which pipeline to run.

## Implicit END
Any node that has **NO outgoing edges** is effectively an END node (in some configs), but it's strongly recommended to explicitly route to `END` for clarity.

## Quick Summary

**1-Line Recall:** **You can exit the graph from any node (Conditional END) and branch immediately upon entry (Conditional Entry Point).**
