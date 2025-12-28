# Graph Analysis & Properties

**Core Definition:** Techniques to mathematically verify your graph before running it.

**Why it Matters:** Finding a bug at compile time is 100x cheaper than finding it in production.

## 1. Validation Logic
When you call `.compile()`, LangGraph runs checks:
-   **Start Check:** Is an entry point defined?
-   **Orphan Check:** Are there nodes that can never be reached?
-   **Sink Check:** Are there nodes (except `END`) that allow no exit?

## 2. Cyclomatic Complexity
A measure of how many paths exist through your code.
-   **High Complexity:** A graph with 50 conditional edges is hard to test.
-   **Mitigation:** Break it into **Subgraphs**.

## 3. Determinism
-   **Deterministic Graph:** Given Input X, always produces Output Y. (DAGs are usually deterministic).
-   **Non-Deterministic Graph:** Depends on LLM choice or Tool output (Agents are non-deterministic).

## 4. Deadlock Analysis
In parallel execution (`Fan-Out`), can the graph get stuck?
-   *Scenario:* Branch A waits for Branch B, but Branch B failed.
-   *LangGraph Solution:* The "Superstep" model prevents traditional threading deadlocks, but logical deadlocks (infinite retry loops) are still possible.

## Quick Summary

**1-Line Recall:** **Use `.compile()` to catch structural errors; keep graph complexity low by using subgraphs when the topology gets too messy.**
