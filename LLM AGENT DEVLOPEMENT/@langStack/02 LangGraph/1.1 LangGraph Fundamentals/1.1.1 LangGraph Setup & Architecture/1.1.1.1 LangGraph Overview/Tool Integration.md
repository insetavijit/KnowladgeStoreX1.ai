# Tool Integration

**Core definition:** **Tool Integration** involves connecting LLMs to external functions (APIs, calculators, search engines) so the graph can perform actions in the real world.

**Position in ecosystem:**
Tools are the "hands" of the agent. LangGraph provides a `ToolNode` to simplify executing these tools safely.

**Key idea:**
- **Binding:** Attaching tool definitions (Schemas) to the LLM.
- **Calling:** The LLM outputs a structured request (JSON).
- **Executing:** The `ToolNode` runs the Python function.
- **Reporting:** The result goes back into the `State`.

## Essential Characteristics

**1. ToolNode:** A pre-built LangGraph node that takes a list of tools and executes them based on LLM requests.
**2. State-Based:** Output from tools is appended to the `messages` list in the state.
**3. Error Handling:** If a tool crashes, the graph can catch it and ask the LLM to retry.

## Code Gist

```python
from langgraph.prebuilt import ToolNode

# Define tools
tools = [search_web, get_weather]

# Bind to model
model_with_tools = model.bind_tools(tools)

# Create Node
tool_node = ToolNode(tools)

# Add to Graph
workflow.add_node("tools", tool_node)
```

## Quick Summaries

**30-second version:** You give the agent a toolbox. When the agent says "I need a hammer," LangGraph pauses, grabs the hammer (function), uses it, and tells the agent what happened. The agent then continues its work with that new information.

**One-line recall:**
**Tools extend the agent's capabilities beyond just text generation.**

---

## Linked Concepts
- [[Nodes & Edges]]
- [[Control Flow & Routing]]
- [[State Management]]

---
**Last updated:** December 2025
