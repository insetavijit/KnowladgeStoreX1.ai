# Node Types

**Core Definition:** While LangGraph treats all nodes as generic functions `(state) -> update`, we semantically categorize them by their *function* in the agent architecture.

## 1. Computation Nodes (The "Doers")
These nodes perform work but don't usually interact with external systems or LLMs directly (or if they do, it's deterministic).
-   **Example:** `summarize_text`, `extract_json`, `format_report`.
-   **Role:** Transform data within the state.

## 2. LLM Nodes (The "Thinkers")
These nodes call an LLM to reason or generate content.
-   **Example:** `agent_node`, `generate_answer`.
-   **Role:** Inject intelligence. They usually read the `messages` history and append a new `AIMessage`.

## 3. Tool Nodes (The "Acters")
A special node provided by LangGraph (`ToolNode`) that executes tools requested by the LLM.
-   **Example:** `tools_node`.
-   **Behavior:** It scans the last message for `tool_calls`. If found, it runs the mapping function and appends a `ToolMessage`.

## 4. Router Nodes (The "Deciders")
These aren't always "real" nodes in the graph; they are often **Conditional Edges**.
-   **Logic:** `should_continue(state) -> "next_node"`.
-   **Role:** Direct traffic. They don't typically modify the state; they just read it to decide where to go next.

## 5. Human-in-the-Loop Nodes
Nodes designed to pause execution.
-   **Interrupts:** You can check point *before* such a node runs.
-   **Role:** Allow a human to inspect/modify state before approving an action.

## Functional vs Semantic
-   *Structurally*, all these are just Python functions.
-   *Semantically*, distinguishing them helps you design clean topologies (e.g., "Think -> Act -> Observe" is "LLM Node -> Tool Node -> LLM Node").

## Quick Summary

**1-Line Recall:** **Nodes are categorized by role: Thinkers (LLM), Doers (Tools), Deciders (Routers), and Transformers (Code).**
