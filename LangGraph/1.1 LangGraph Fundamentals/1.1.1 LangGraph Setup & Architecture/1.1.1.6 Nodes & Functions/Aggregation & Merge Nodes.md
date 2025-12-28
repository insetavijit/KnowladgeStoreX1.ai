# Aggregation & Merge Nodes

**Core Definition:** Nodes that run after parallel branches to reconcile disparate state updates.

## The Fan-Out / Fan-In Problem
If Node A splits into Node B and Node C, and both run in parallel:
-   B returns `{"score": 5}`.
-   C returns `{"score": 10}`.
-   Who wins?

## 1. The Reducer (Implicit Merging)
The conflict is resolved by the `State` definition, usually `operator.add` or `last_write_wins`. You don't always need a specific node to merge them if the state handles it.

## 2. The Aggregator Node (Explicit Merging)
If you need complex logic (e.g., "Take the average of the scores"), you create a node that runs *after* B and C.

```python
def aggregator(state):
    # Assume B and C wrote to 'results' list
    avg = sum(state["results"]) / len(state["results"])
    return {"final_score": avg}

workflow.add_edge(["B", "C"], "aggregator")
```

## Synchronization
The aggregator waits for **ALL** incoming active branches to finish before running. This is a "Barrier" synchronization.

## Quick Summary

**1-Line Recall:** **Merge nodes act as synchronization barriers; they run only when all parallel predecessors have finished and use logic to combine their results.**
