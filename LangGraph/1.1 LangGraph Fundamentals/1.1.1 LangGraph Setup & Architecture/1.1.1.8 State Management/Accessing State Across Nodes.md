# Accessing State Across Nodes

**Core Definition:** Patterns for how different nodes consume shared data.

## The "Global Blackboard" Model
Think of State as a whiteboard in the room. Node A writes to it. Node B reads from it.
-   **Pull Pattern:** Node B explicitly reads `state["user_input"]`.
-   **Push Pattern:** (Not really used in LangGraph). Nodes don't "send" data to B; they update the Blackboard.

## Dependency Injection (via State)
If Node B needs the result of Node A, Node A MUST write it to the State.
-   *Implicit Dependency:* Node B assumes `state["a_result"]` exists.
-   *Safety:* Use structural validation (TypedDict) to ensure `a_result` is a required field, or check for presence.

## Context Passing
Use `config` (separate from State) for static context that doesn't change (User ID, API Keys).
Use `State` for dynamic context (Conversation history).

## Quick Summary

**1-Line Recall:** **Nodes communicate indirectly via the State; if Node B needs data from Node A, Node A must write it to the State Schema.**
