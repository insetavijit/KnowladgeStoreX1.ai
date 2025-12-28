# Shared vs Private State

**Core Definition:** Distinguishing between what everyone sees (Global) and what a sub-agent keeps to itself (Private).

## All State is Global (by default)
In a standard `StateGraph`, every node has access to every key in the schema. There is no access control.

## Subgraphs for Privacy
To achieve "Private State," you use **Subgraphs**.
1.  **Parent Graph:** Has `GlobalState`.
2.  **Child Graph:** Has `ChildState` (which might contain Global fields + private fields).
3.  **Encapsulation:** The Parent graph *cannot* see the private fields of the Child. It only sees the final output.

## Why Encapsulate?
If you have a complex "Researcher" agent, the main "Supervisor" agent doesn't need to know about the Researcher's internal scratchpad, browser tabs, or temporary errors. It just wants the final report.

## Quick Summary

**1-Line Recall:** **Use Subgraphs to create 'Private Scope'; the parent graph only sees the inputs and outputs of the subgraph, not the internal state churn.**
