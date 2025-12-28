# Long-Running Workflows

**Core Definition:** Agents that run for hours, days, or weeks.

## The Problem
You can't keep a Python process execution `graph.invoke()` open for 3 days. It will crash or timeout.

## The Solution: Checkpoints & Queues
1.  **Background Workers:** Use a queue (Celery, temporal).
2.  **Execution Loop:**
    -   Worker picks up task.
    -   Worker runs `graph.invoke(..., config=thread)`.
    -   Graph runs until it hits an async wait or "sleep" node (conceptually).
    -   Worker saves state (checkpoint) and exits.
    -   Cron job wakes up later, resumes graph from checkpoint.

## LangGraph Cloud
This infrastructure helps manage long-running async agents automatically, but you can build it yourself using the Checkpointer + Thread ID pattern.

## Quick Summary

**1-Line Recall:** **Long-running workflows rely on persisting state to a database and resuming execution periodically using the matching `thread_id`.**
