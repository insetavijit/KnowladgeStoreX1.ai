# Memory Efficiency

**Core Definition:** Keeping the state payload small to reduce latency and token costs.

## The Problem: Infinite Append
If you just keep appending messages, eventually:
1.  Context Window Overflow (LLM crash).
2.  Slow Network Transfer (sending 1MB of JSON).
3.  High Cost ($$$).

## Strategy 1: Truncation
Only keep the last N messages.
*Note: This must be done logic-wise, usually by a "Memory Management" node that deletes old messages.*

## Strategy 2: Summarization
Periodically ask an LLM to "Compress this conversation into a summary" and replace the history with `[Summary, ...new_messages]`.

## Strategy 3: Offloading
Don't put large documents in the State.
-   **Bad:** `state["docs"] = [full_text_of_100_pdfs]`
-   **Good:** `state["doc_ids"] = [1, 2, 3]`. Fetch text only when needed, or keep in a vector store.

## Quick Summary

**1-Line Recall:** **State is hot memory; keep it lean by referencing large data (IDs) rather than embedding it, and actively prune message history.**
