# When to Use Chains

**Core Definition:** The right tool for the job.

## Recommended Use Cases

1.  **Simple RAG:** Retrieve -> augment -> generate. No loops.
2.  **Data Extraction:** Input text -> Output JSON.
3.  **Classification:** Input text -> Label.
4.  **Prototyping:** Checking if a prompt works.

## Why?
Overengineering is bad. If a straight line works, don't build a cycle.

## Quick Summary

**1-Line Recall:** **Use Chains for stateless, linear, input-to-output transformations where no looping or complex state persistence is required.**
