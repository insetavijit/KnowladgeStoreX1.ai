# When to Use LangGraph

**Core definition:** A guide on choosing the right tool. Use LangGraph when you need **cycles (loops)**, **persistence**, or **complex control flow**.

**Position in ecosystem:**
Don't use a sledgehammer to crack a nut. Don't use LangGraph for a simple prompt.

**Key idea:**
- **Complexity Spectrum:**
    1.  **Prompt:** Simple Q&A.
    2.  **Chain:** Sequence of steps (RAG).
    3.  **Router:** Choosing between 2 chains.
    4.  **Agent (LangGraph):** Loops, Memory, Tools.

## Decision Matrix

| Feature Need | Use LangChain (Chain) | Use LangGraph |
| :--- | :--- | :--- |
| **Input -> Output** | Yes | Overkill |
| **Retries / Loops** | No (Hard) | Yes (Native) |
| **State across steps** | No | Yes |
| **Human Approval** | No | Yes |
| **Parallelism** | Runnables (RunnableParallel) | Graph Nodes |

## Good Fit Scenarios
*   Coding Assistant (Write -> Test -> Fix Loop).
*   Customer Support Bot (Auth -> Lookup -> Reply -> Handoff).
*   Research Agent (Search -> Read -> Summarize -> Repeat).

## Poor Fit Scenarios
*   Simple Text Summarizer.
*   Basic Chatbot without tools.
*   One-off data extraction script.

## Quick Summaries

**30-second version:** If you can draw your workflow as a straight line from left to right, use a Chain. If your drawing has circles, arrows pointing back, or intricate decision diamonds, use LangGraph.

**One-line recall:**
**Use LangGraph for cycles, persistence, and complex agency.**

---

## Linked Concepts
- [[Graphs vs Chains]]
- [[Examples & Case Studies]]
- [[Role in Agent Stack]]

---
**Last updated:** December 2025
