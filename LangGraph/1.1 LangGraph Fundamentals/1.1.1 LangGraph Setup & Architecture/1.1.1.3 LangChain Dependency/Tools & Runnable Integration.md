# Tools & Runnable Integration

**Core Definition:** This section covers how **Tools** (actions) are defined and how **Runnables** (chains) are composed to create the logic inside LangGraph nodes.

**The "Do" Component:** If Models are the "Brain", Tools are the "Hands".

## Tool Definition

### 1. The `@tool` Decorator
The simplest way to create a tool. It uses Python type hints and docstrings to generate the tool schema for the LLM.

```python
from langchain_core.tools import tool

@tool
def calculate_tax(amount: float, rate: float = 0.1) -> float:
    """Calculates sales tax based on amount and rate."""
    return amount * rate
```

### 2. `StructuredTool`
For more complex setup or when wrapping existing functions without decorators.
-   Allows explicit definition of `args_schema` using Pydantic models.
-   Useful for validation logic.

### 3. Tool Exception Handling
Crucial for agents. If a tool fails, you don't want the agent to crash; you want it to see the error and try again.
-   **`handle_tool_error=True`**: The tool returns the error message as a string to the model instead of raising an exception.

## Runnable Integration (LCEL)

The **LangChain Expression Language (LCEL)** is used to define the internal processing of a node.

### 1. `RunnableSequence` (`|`)
Pipes output from one step to the next.
`chain = prompt | model | parser`

### 2. `RunnableMap` (`RunnableParallel`)
Runs multiple steps in parallel and merges results.
```python
# Run retrieval and question pass-through in parallel
context = RunnableParallel(
    context=retriever,
    question=RunnablePassthrough()
)
```

### 3. Binding Runtime Args (`.bind()`)
Used to attach tools or stop sequences to a model at runtime.
`llm_with_tools = llm.bind_tools([calculate_tax])`

## LangGraph connection

In a **ToolNode**:
1.  The node receives a `ToolMessage` request.
2.  It identifies the tool by name.
3.  It executes the corresponding `Runnable` (the tool function).
4.  It returns the output as a `ToolMessage`.

## Quick Summary

**1-Line Recall:** **Tools define what an agent CAN do (@tool); Runnables define the FLOW of data (\|) inside the agent's steps.**
