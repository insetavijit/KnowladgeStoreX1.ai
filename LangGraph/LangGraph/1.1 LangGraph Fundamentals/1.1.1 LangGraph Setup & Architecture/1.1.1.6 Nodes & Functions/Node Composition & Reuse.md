# Node Composition & Reuse

**Core Definition:** Writing nodes that are generic enough to be used in multiple different graphs.

## The Problem: Hardcoded State Keys
If your node looks like this:
```python
def my_node(state):
    return {"my_specific_key": state["other_key"] + 1}
```
It can *only* be used in graphs with that exact schema.

## 1. Factory Pattern (Configurable Nodes)
Write a function that *returns* a node function.

```python
def create_summary_node(input_key, output_key):
    def node(state):
        data = state[input_key]
        summary = summarize(data)
        return {output_key: summary}
    return node

# Usage
workflow.add_node("summary_A", create_summary_node("doc_a", "summary_a"))
workflow.add_node("summary_B", create_summary_node("doc_b", "summary_b"))
```

## 2. The `Runnable` Protocol
Since Nodes are Runnables, you can compose them using LangChain chains (`|`).

```python
# A standard LangChain chain
chain = prompt | model | parser

# Use the chain directly as a node!
workflow.add_node("my_chain_node", chain)
```
*Note: The chain must accept a dict and return a dict compatible with the state.*

## Quick Summary

**1-Line Recall:** **Use Factory Functions to create configurable nodes that act as "Generic Components," decoupling logic from specific state keys.**
