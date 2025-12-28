# Control Flow & Routing

**Core definition:** **Control Flow** is the logic that dictates the sequence of execution in a graph. **Routing** is the specific mechanism (using conditional edges) to choose between multiple downstream paths.

**Position in ecosystem:**
This is what makes LangGraph "agentic." Without routing, you just have a fancy pipeline. Routing allows the agent to make decisions.

**Key idea:**
- **Deterministic Flow:** Hardcoded paths (A always goes to B).
- **Conditional Flow:** Logic-based paths (A goes to B *if* x > 5, else C).

## Essential Characteristics

**1. Routing Functions:** Small, read-only functions that inspect state and return the *name* of the next node.
**2. Branching:** Splitting execution into one of several paths (or even parallel paths).
**3. Tool Use:** The most common routing pattern—LLM decides "I need a tool" -> Router sends flow to "ToolNode"; otherwise -> END.
**4. Human-in-the-Loop:** Routing can pause execution and wait for a "resume" signal.

## Common Patterns

### The "Agent Loop" Pattern
1.  **Agent Node:** Generates thought/response.
2.  **Router:** Checks `state.last_message`.
    - Does it contain a tool call? -> **Go to Tool Node**.
    - Is it a final answer? -> **Go to END**.
3.  **Tool Node:** Executes tool.
4.  **Edge:** Loops back to **Agent Node**.

## Logic Example

```python
def route_step(state):
    # Check if the last message has tool calls
    if state["messages"][-1].tool_calls:
        return "tools"
    else:
        return "end"

# In graph definition:
workflow.add_conditional_edges("chatbot", route_step)
```

## Quick Summaries

**30-second version:** Control flow is the traffic system. Routing is the traffic light changing from red to green based on whether there are cars waiting (state). It allows the application to react to data dynamically rather than following a script blindly.

**One-line recall:**
**Routing enables the graph to make dynamic decisions at runtime.**

---

## Linked Concepts
- [[Nodes & Edges]]
- [[Tool Integration]]
- [[Loops & Iteration]]

---
**Last updated:** December 2025
