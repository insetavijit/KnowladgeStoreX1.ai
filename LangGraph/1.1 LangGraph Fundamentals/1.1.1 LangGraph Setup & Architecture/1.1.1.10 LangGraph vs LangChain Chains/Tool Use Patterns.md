# Tool Use Patterns

**Core Definition:** How the agent invokes external functions.

## Chains: The "ReAct" Agent
In LangChain (legacy), tool use is hidden inside the `AgentExecutor` class.
-   It parses the LLM output.
-   It runs the tool.
-   It passes the output back.
-   **Problem:** Customizing this loop (e.g., "Ask user for confirmation before running tool") is very hard.

## Graphs: Explicit Tool Nodes
In LangGraph, you just add a node.

```python
workflow.add_node("tools", ToolNode(tools))
workflow.add_conditional_edges("agent", should_continue)
```

-   **Freedom:** You can put a "Human Approval" node *between* the Agent and the Tool.
-   **Clarity:** The graph diagram shows exactly where tools are called.

## Quick Summary

**1-Line Recall:** **LangGraph exposes Tool execution as a standard node, allowing you to insert logic (approval, modification) before or after the tool runs.**
