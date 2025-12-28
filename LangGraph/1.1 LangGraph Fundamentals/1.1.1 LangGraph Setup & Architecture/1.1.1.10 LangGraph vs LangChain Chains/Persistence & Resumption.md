# Persistence & Resumption

**Core Definition:** Stopping and Starting.

## Chains: Ephemeral
Run it, it finishes. If power goes out, it's gone.
-   To resume, you have to manually re-feed the history into a new chain run.

## Graphs: Persistent
-   **Checkpointing:** Automatic saving to DB.
-   **Resumption:** Native `thread_id` support. The graph knows *exactly* where it left off, including internal variables that aren't just "messages".

## Human-in-the-Loop
This is only possible with Graphs (or very hacked Chains).

## Quick Summary

**1-Line Recall:** **LangGraph has native persistence (checkpointing), enabling long-running or interrupted workflows; Chains are designed to be ephemeral.**
