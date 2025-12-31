# Legacy Agent Frameworks

**Core Definition:** `AgentExecutor`.

## The Old Way
LangChain had `AgentExecutor`, which was a hardcoded loop.
-   It was "good enough" for simple ReAct agents.
-   It was nearly impossible to debug or modify.

## The New Way (LangGraph)
`create_react_agent` in LangGraph builds a semantic graph `Agent -> Tools -> Agent`.
-   It does the same thing as `AgentExecutor`.
-   **Difference:** It operates on a Graph. You can inspect it, add nodes to it, or delete edges.

## Migration
LangChain is actively recommending moving all Agents to LangGraph.

## Quick Summary

**1-Line Recall:** **Legacy 'AgentExecutor' is replaced by LangGraph's prebuilt agents, which offer the same functionality but on a transparent, modifiable graph architecture.**
