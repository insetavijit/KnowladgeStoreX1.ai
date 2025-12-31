# Graphs vs Chains

**Core definition:** **Graphs** are non-linear workflows that support **loops, branches, and shared state**, whereas **Chains** are **linear, fixed sequences** of steps.

**Position in ecosystem:**
Graphs (LangGraph) are for complex, adaptive agents. Chains (LangChain) are for simple, predictable pipelines.

**Key idea:**
- **DAO (Linear):** A -> B -> C (Simple, Fast)
- **Cyclic (Graph):** A -> B -> (if x) -> C -> (loop) -> A (Flexible, Adaptive)

## Essential Characteristics

**1. Cyclic Capability:** Graphs can loop back to previous steps (essential for agentic "retry" or "refine" behaviors).
**2. Conditional Branching:** Dynamic path selection based on state (e.g., "Tool needed?" -> Yes/No).
**3. State Persistence:** Graphs maintain memory across the entire lifecycle, unlike simple pass-through chains.
**4. Complexity Handling:** Better suited for ambiguity where the next step isn't known ahead of time.

## Comparative Table

| Feature | LangChain Chains | LangGraph Graphs |
| :--- | :--- | :--- |
| **Structure** | Linear (DAG) | Cyclic & Non-linear |
| **Control Flow** | Hardcoded sequence | Dynamic (Router/Edge) |
| **State** | Transient (per run) | Persistent (global state) |
| **Use Case** | RAG, ETL, Simple Scripts | Autonomous Agents, Chatbots |
| **Debugging** | Easy (step-by-step) | Requires state inspection |

## Real-World Analogy

- **Chain:** A cooking recipe. You must follow step 1, then step 2, then step 3. You don't go back to step 1 if the oven is cold; you strictly follow the list.
- **Graph:** A chef cooking. The chef tastes the soup (node). If it needs salt (decision), they add salt (branch) and taste again (loop). If it's good, they serve it (end).

## Quick Summaries

**30-second version:** Use Chains for straight lines where Step B always follows Step A. Use Graphs for circles and trees where the agent might need to repeat a step, choose between different paths, or maintain long-term memory during a conversation.

**One-line recall:**
**Chains are for pipelines; Graphs are for agents.**

---

## Linked Concepts
- [[What is LangGraph]]
- [[LLM AGENT DEVLOPEMENT/@langStack/02 LangGraph/1.1 LangGraph Fundamentals/1.1.1 LangGraph Setup & Architecture/1.1.1.1 LangGraph Overview/When to Use LangGraph]]
- [[Loops & Iteration]]

---
**Last updated:** December 2025
