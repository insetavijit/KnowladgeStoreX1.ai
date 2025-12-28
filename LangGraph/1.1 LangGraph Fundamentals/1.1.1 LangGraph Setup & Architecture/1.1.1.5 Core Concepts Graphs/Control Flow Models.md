# Control Flow Models

**Core Definition:** Common patterns for arranging logic in a graph. These are the "Design Patterns" of agent engineering.

## 1. The Chain (Sequential)
`A -> B -> C`
-   **When:** Tasks must happen in order.
-   **Example:** Research -> Write -> Edit.

## 2. The Loop (Iterative)
`A -> B -> A`
-   **When:** You need to refine or correct something.
-   **Example:** Generate Code -> Test -> (Fail) -> Generate Code ...

## 3. The Branch (Conditional)
`A -> (B OR C)`
-   **When:** You need to make a choice.
-   **Example:** Query Classifier -> (rag_node OR talk_node).

## 4. The Fork-Join (Parallel)
`A -> (B AND C) -> D`
-   **When:** Independent tasks can be sped up.
-   **Example:** A -> (Search Google AND Search Wikipedia) -> Summarize.

## 5. The Fallback (Exception Handling)
`A -> B (Error) -> C -> END`
-   **When:** A step is flaky.
-   **Example:** Tool Call (Fail) -> Fallback Model -> END.

## Explicit Control

In LangGraph, you don't write `if/else` inside a massive function. You lift that control flow **up** into the graph edges.
-   *Code:* `if x: do_y()`
-   *Graph:* `add_conditional_edges("x", router_function)`

This makes the logic **visible** to tooling (LangSmith) and easier to reason about.

## Quick Summary

**1-Line Recall:** **Control flow models (Chain, Loop, Branch, Parallel) are the primitives you mix and match to build complex agent behavior.**
