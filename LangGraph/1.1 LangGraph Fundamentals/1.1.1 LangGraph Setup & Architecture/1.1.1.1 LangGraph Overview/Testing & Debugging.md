# Testing & Debugging

**Core definition:** **Testing** verifies the agent behaves correctly. **Debugging** involves investigating the trace of graph execution to understand *why* it made a specific decision.

**Position in ecosystem:**
Agents are non-deterministic. Traditional unit tests usually aren't enough; you need tracing tools (LangSmith) and visualizers.

**Key idea:**
- **LangSmith Tracing:** Logs every step, input, output, and latency.
- **Time Travel Debugging:** Replay a failed production run locally to fix the bug.
- **Unit Testing:** Mocking nodes to test edge routing logic.

## Essential Characteristics

**1. Observability:** Seeing the full "thought process" of the agent, not just the final answer.
**2. Deterministic Replay:** Feeding the same historic state to a node to see if the fix works.
**3. Visualizer:** Generating a graph image (`graph.get_graph().draw_mermaid_png()`) to verify the topology.

## Tools of the Trade

- **`print(state)`**: The caveman method (still useful).
- **LangSmith**: The pro method (full GUI traces).
- **Mermaid Diagrams**: For checking if your wiring is correct.

## Quick Summaries

**30-second version:** Debugging an agent is hard because it's like a "black box." LangGraph opens the box by logging every single step. You can see exactly what the agent "thought" at node 3, why it chose path B, and allows you to "time travel" back to that moment to fix it.

**One-line recall:**
**LangGraph makes agent logic observable and replayable.**

---

## Linked Concepts
- [[Error Handling & Recovery]]
- [[State Management]]
- [[Performance & Cost]]

---
**Last updated:** December 2025
