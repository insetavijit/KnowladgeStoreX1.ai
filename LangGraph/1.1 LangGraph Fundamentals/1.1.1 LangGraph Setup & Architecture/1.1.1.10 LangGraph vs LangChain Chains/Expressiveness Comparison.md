# Expressiveness Comparison

**Core Definition:** What *can* you build with X vs Y?

## What Chains Can Do
-   Sequence: `A -> B -> C`
-   Parallel: `A -> (B, C) -> D`
-   Conditional (limited): `RunnableBranch` (deprecated-ish) or custom routers.

## What Graphs Can Do (That Chains Can't)
-   **Loops:** `A -> B -> A`. Essential for "Retry until success" or "Agentic thought loops".
-   **Complex Branching:** `A` goes to `B` OR `C` OR `D` based on granular logic.
-   **State Accumulation:** A runs, B runs, C runs. D can see what A did, even if B didn't pass it forward explicitly, because it's in the shared State.

## The "Agent" Factor
You *can* build an agent in a Chain (using `AgentExecutor`), but it's a "Black Box" loop hardcoded inside the library. In LangGraph, you *draw* the loop yourself.

## Quick Summary

**1-Line Recall:** **Chains are limited to Directed Acyclic Graphs (DAGs); LangGraph supports Cycles and arbitrary control flow, making it Turing Complete-ish.**
