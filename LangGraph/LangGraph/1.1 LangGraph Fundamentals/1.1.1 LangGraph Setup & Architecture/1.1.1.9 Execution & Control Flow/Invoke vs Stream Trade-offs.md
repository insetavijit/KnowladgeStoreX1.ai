# Invoke vs Stream Trade-offs

**Core Definition:** Deciding whether to wait for the whole result or handle a stream of events.

## When to use `invoke()` / `ainvoke()`
1.  **Backend Tasks:** Cron jobs, data processing pipelines.
2.  **Simple Scripts:** Testing or prototyping.
3.  **Atomic Operations:** "Classify this email" (where partial results aren't useful).
4.  **Pros:** Simpler code, simpler error handling.

## When to use `stream()` / `astream()`
1.  **Chatbots:** Users expect to see the bot "typing".
2.  **Long Processes:** "Steps 1/5 complete..." feedback.
3.  **Debugging:** Seeing which node caused the crash *as it happens*.
4.  **Pros:** Better UX.
5.  **Cons:** Complex client-side handling (need to consume an iterator).

## Performance
`stream` converts the execution into a generator. It doesn't make the *graph* slower, but network overhead for many small chunks is higher than one big chunk.

## Quick Summary

**1-Line Recall:** **Default to `stream` for user-facing applications to reduce perceived latency; use `invoke` for headless automation.**
