# Unconditional Edges

**Core Definition:** A hardcoded link between two nodes. It asserts sequential dependency (B cannot start until A finishes).

## Syntax
```python
workflow.add_edge("source_node", "target_node")
```

## Chains via Edges
To build a classic "Prompt | Model | Parser" chain in LangGraph, you just stitch nodes together with conditional edges.

```python
workflow.add_edge(START, "format_prompt")
workflow.add_edge("format_prompt", "invoke_model")
workflow.add_edge("invoke_model", "parse_output")
workflow.add_edge("parse_output", END)
```

## From "Any" Node
You can route from ANY node (LLM, Tool, etc.) to ANY other node, as long as the State schema matches.

## Visual Representation
In diagrams, these are solid, labeled lines.
`[Format] --> [Model]`

## When NOT to use them
If there is ANY chance you might want to stop, loop, or skip a step, you cannot use `.add_edge()`. You must use `.add_conditional_edges()`.

## Quick Summary

**1-Line Recall:** **Use `add_edge(A, B)` to create a rigid, linear sequence where B always follows A.**
