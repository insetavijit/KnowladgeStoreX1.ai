# Node Naming & Documentation

**Core Definition:** Writing nodes that explain themselves. The graph visualization uses the node name, so it is your primary UI for debugging.

## Naming Rules

1.  **Unique Strings:** The string key must be unique in the graph. `workflow.add_node("search", ...)`
2.  **Verbs vs Nouns:**
    -   *Verb:* `retrieve_docs` (Focus on action).
    -   *Noun:* `retriever` (Focus on role).
    -   *Result:* LangGraph displays this string in the diagram. **Verbs usually read better** as a flow: `Start -> Retrieve -> Grade -> End`.

## Docstrings
LangGraph doesn't (yet) display docstrings in the visualizer, but your teammates read them.

```python
def generate_answer(state: State):
    """
    Reads the 'documents' from state and synthesizes an answer.
    
    Inputs: state['documents'], state['question']
    Outputs: state['answer']
    """
```

## Type Hinting
Always hint the inputs and outputs. It serves as documentation for the data flow.

```python
def my_node(state: InputState) -> OutputUpdate:
```

## Quick Summary

**1-Line Recall:** **Name nodes with strong Verbs (e.g., 'generate', 'grade', 'search') so the visual graph tells a coherent story.**
