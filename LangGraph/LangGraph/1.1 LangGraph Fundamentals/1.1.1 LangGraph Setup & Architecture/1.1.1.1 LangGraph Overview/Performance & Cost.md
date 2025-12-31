# Performance & Cost

**Core definition:** Managing the **latency (speed)** and **token usage (cost)** of your graph executions.

**Position in ecosystem:**
Agents can loop infinitely. Without cost controls, a simple "hello" could turn into $50 of API calls.

**Key idea:**
- **Recursion Limits:** Stop the graph after N steps globally.
- **Token Tracking:** Monitoring input/output tokens per node.
- **Latency Optimization:** Using parallelism to run nodes constantly.

## Essential Characteristics

**1. Cognitive Architecture:** Designing the graph to use "cheaper" models for simple routing and "expensive" models only for complex reasoning.
**2. Batching:** Grouping inputs to save round-trips.
**3. Caching:** Storing results of expensive tool calls (like search) if the query is repeated.

## Cost Drivers within LangGraph

*   **Loops:** Every loop iteration typically involves a new LLM call.
*   **State History:** Sending the full chat history every time consumes context window tokens.
*   **Strategy:** Summarize or trim old history in the `State` to keep payloads small.

## Quick Summaries

**30-second version:** Agents are expensive interns. They charge you for every word they read and write. LangGraph helps you manage the budget by setting limits on how long they can work (recursion limit) and optimizing their workflow (parallelism) so they finish faster.

**One-line recall:**
**Efficient graphs optimize for minimal tokens and maximum speed.**

---

## Linked Concepts
- [[Loops & Iteration]]
- [[Parallelism & Concurrency]]
- [[LangGraph/1.1 LangGraph Fundamentals/1.1.1 LangGraph Setup & Architecture/1.1.1.1 LangGraph Overview/When to Use LangGraph]]

---
**Last updated:** December 2025
