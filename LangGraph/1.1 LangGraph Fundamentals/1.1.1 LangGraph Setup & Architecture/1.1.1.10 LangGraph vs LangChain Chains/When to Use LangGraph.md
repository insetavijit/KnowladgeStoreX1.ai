# When to Use LangGraph

**Core Definition:** The *only* tool for Agents.

## Recommended Use Cases

1.  **Agents:** Anything that uses Tools.
2.  **Chatbots:** Anything with memory/history.
3.  **Complex Logic:** "If X, do Y, else loop back to Z."
4.  **Human-in-the-Loop:** "Stop and ask user."
5.  **Multi-Modal Flows:** Parallel processing of images and text.

## Why?
Agents are inherently cyclic (Think -> Act -> Observe -> Think). Chains cannot express this cycle cleanly.

## Quick Summary

**1-Line Recall:** **Use LangGraph for practically any AI application that isn't a simple one-shot script; specifically for Agents, cyclic workflows, and persistent applications.**
