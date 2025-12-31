# State Management Differences

**Core Definition:** How data is handled between steps.

## Chains: "Pass the Ball"
In a Chain, Step 1 returns an output. Step 2 receives that output as input.
-   If Step 3 needs Step 1's output, Step 2 MUST pass it along.
-   This leads to "Prop drilling" or messy input/output maps.

## Graphs: "Shared Whiteboard"
In LangGraph, there is a central **State Schema**.
-   Step 1 writes to `state["summary"]`.
-   Step 2 writes to `state["keywords"]`.
-   Step 3 reads both from `state`.
-   Step 2 didn't need to know about "summary".

## Typed vs Implicit
-   **Chains:** Often just generic dictionaries. Hard to debug "what keys are available?".
-   **Graphs:** Ideally `TypedDict`. You know exactly what the memory looks like.

## Quick Summary

**1-Line Recall:** **Chains rely on implicit message passing (inputs/outputs); Graphs rely on a centralized, typed State object accessible to all nodes.**
