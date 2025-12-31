# Role in Agent Stack

**Core definition:** **LangGraph** serves as the **Orchestration Layer** / Control Plane of a modern AI application stack.

**Position in ecosystem:**
It sits between the raw **LLM (Brain)** and the **Application UI**. It coordinates the tools, memory, and logic.

**Key idea:**
- **LLM:** The reasoning engine (GPT-4, Claude).
- **LangChain:** The interface for prompts and tools.
- **LangGraph:** The architecture that ties them together into a workflow.
- **LangSmith:** The monitoring dashboard for the workflow.

## The Stack Hierarchy

1.  **User Interface (frontend):** React/Streamlit chat.
2.  **API Layer:** FastAPI / LangServe.
3.  **Orchestrator (LangGraph):** Manages state, decisions, loops.
4.  **Components (LangChain):**
    *   **Tools:** Search, Calculator.
    *   **Memory:** Vector DBs.
5.  **Model Layer:** OpenAI / local LLMs.

## Why it matters
Separating the "Orchestrator" from the "Prompting" allows you to swap models easily while keeping the complex business logic (the graph) intact.

## Quick Summaries

**30-second version:** In a company, the LLM is the talented employee. LangChain is the desk and computer they use. LangGraph is the Manager who tells them what to do, checks their work, and coordinates with other departments.

**One-line recall:**
**LangGraph is the operating system for the agent Application.**

---

## Linked Concepts
- [[What is LangGraph]]
- [[LangGraph/1.1 LangGraph Fundamentals/1.1.1 LangGraph Setup & Architecture/1.1.1.1 LangGraph Overview/When to Use LangGraph]]
- [[LangChain Dependency]]

---
**Last updated:** December 2025
