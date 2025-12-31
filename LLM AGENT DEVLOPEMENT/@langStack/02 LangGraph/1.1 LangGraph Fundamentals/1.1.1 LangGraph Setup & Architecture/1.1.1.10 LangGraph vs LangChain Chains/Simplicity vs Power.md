# Simplicity vs Power

**Core Definition:** The trade-off between Ease of Start and Ceiling of Capability.

## Chains: High Simplicity
-   **Code:** One line (`chain = prompt | llm`).
-   **Mental Load:** Low. Just a list of steps.
-   **Ceiling:** Low. As soon as you need a loop, it gets hacky.

## Graphs: High Power
-   **Code:** Verbose. 10+ lines to define nodes, add edges, compile.
-   **Mental Load:** Higher. You need to think about State Schemas and Reducers.
-   **Ceiling:** Very High. Can build autonomous coding agents, multi-agent swarms, etc.

## The Recommendation
-   Start with a Chain for simple RAG.
-   Refactor to a Graph the moment you think "I need to check the output and maybe try again."

## Quick Summary

**1-Line Recall:** **Chains are excellent for simple, linear sequences; Graphs introduce boilerplate but are necessary for any complexity involving loops or decisions.**
