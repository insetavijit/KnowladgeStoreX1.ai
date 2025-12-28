# Directed Acyclic Graphs (DAGs)

**Core Definition:** A **DAG** is a graph that moves in one direction (Directed) and never loops back on itself (Acyclic).

**Why it Matters:** DAGs represent **deterministic, finite workflows**. If your agent has a clear start and a guaranteed end with no "retry loops," it is a DAG.

## Characteristics of a DAG

1.  **Finite Execution:** It is mathematically impossible for a DAG to run forever. It *must* finish.
2.  **Topological Sort:** Nodes can be arranged in a linear line such that all arrows point left-to-right.
3.  **No Feedback Loops:** Information flows downstream only. Step B cannot influence Step A.

## LangGraph & DAGs

While LangChain's `SequentialChain` describes a straight line (List), LangGraph uses DAGs to describe **pipelines with branching**.

### Example Scenario: A Content Publisher

1.  **Node A (Research):** Scrape data.
2.  **Node B (Draft):** Write article.
3.  **Router:** Is it good?
4.  **Node C (Publish):** Push to blog.
5.  **Node D (Archive):** Save to disk.

*This allows branching (maybe we Archive but don't Publish), but we never go back to Research.*

### Code Structure

```python
workflow = StateGraph(State)

workflow.add_node("research", research_node)
workflow.add_node("draft", draft_node)
workflow.add_node("publish", publish_node)

workflow.add_edge("research", "draft")
workflow.add_edge("draft", "publish") # One way street
workflow.add_edge("publish", END)
```

## Benefits of DAGs in AI

1.  **Debuggability:** Easy to trace. If it failed at step 3, you know step 1 and 2 finished.
2.  **Parallelism:** In a DAG, if Node B and Node C both depend on Node A but not on each other, they can run in parallel perfectly.
3.  **Caching:** Results can be cached aggressively because there are no side-effect loops.

## When DAGs Fail (Why we need Cycles)

DAGs cannot handle:
-   "The code failed, try again." (<strong>Retry Loop</strong>)
-   "The answer is vague, think deeper." (<strong>Refinement Loop</strong>)
-   "Chat with the user until they say goodbye." (<strong>Conversation Loop</strong>)

## Quick Summary

**1-Line Recall:** **DAGs are "One-Way Streets" for data; perfect for pipelines and RAG, but insufficient for autonomous agents that need to iterate.**
