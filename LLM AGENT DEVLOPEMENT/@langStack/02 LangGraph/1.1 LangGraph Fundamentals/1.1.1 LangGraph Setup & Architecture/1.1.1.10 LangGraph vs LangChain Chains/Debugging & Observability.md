# Debugging & Observability

**Core Definition:** Understanding *why* it did that.

## Chains: opaque Traces
Debugging a chain often requires looking at a massive nested trace in LangSmith. It's hard to see "Current State" because context is implicit.

## Graphs: Step-by-Step Inspection
You can literally `print(state)` after every node.
-   **Visual:** You can look at the graph diagram to see the path taken.
-   **State:** You see exactly what data was available to the node at that moment.

## Time Travel
LangGraph allows you to rewind execution. Chains do not.

## Quick Summary

**1-Line Recall:** **Graphs are easier to debug because the 'State' at every step is explicit and inspectable, whereas Chains hide context in closure scopes.**
