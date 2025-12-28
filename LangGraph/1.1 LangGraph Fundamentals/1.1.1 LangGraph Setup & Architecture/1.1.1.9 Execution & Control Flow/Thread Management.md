# Thread Management

**Core Definition:** Isolating different conversations or execution runs using unique identifiers.

## The `thread_id`
The primary key for a conversation.
-   **User 1, Chat A:** `thread_id="user1_chatA"`
-   **User 1, Chat B:** `thread_id="user1_chatB"`

## Multi-Tenancy
LangGraph doesn't inherently know about "Users" or "Orgs". It only knows Threads.
You must manage the mapping of `User -> [Threads]` in your own database definition, then pass the correct `thread_id` to LangGraph.

## Checkpoint Namespace
A thread is a linear history of checkpoints.
-   You cannot "merge" two threads.
-   You typically cannot "fork" a thread (unless you manually copy the state to a new thread ID).

## Quick Summary

**1-Line Recall:** **Threads partition state; always use a unique `thread_id` for every distinct conversation or workflow instance to prevent state collision.**
