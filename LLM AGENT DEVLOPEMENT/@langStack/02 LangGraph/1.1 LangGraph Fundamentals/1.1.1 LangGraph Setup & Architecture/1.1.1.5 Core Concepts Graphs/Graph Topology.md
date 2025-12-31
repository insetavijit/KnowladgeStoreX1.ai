# Graph Topology

**Core Definition:** Topology refers to the "shape" of the graph—how nodes and edges are arranged. Different agent architectures correspond to different topologies.

**Why Study This:** When someone describes an agent (e.g., "Supervisor", "Hierarchical", "Router"), they are describing a specific **Topological Pattern**.

## Common Topologies

### 1. The Linear Chain (Pipeline)
`A -> B -> C -> END`
-   **Use Case:** Simple RAG (Retrieve -> Generate).
-   **Properties:** No decisions, high reliability, low autonomy.

### 2. The Loop (ReAct)
`Start -> Model <-> Tool -> End`
-   **Use Case:** General purpose assistants.
-   **Properties:** High autonomy, variable execution time.

### 3. The Router (Fan-Out)
A central node decides which specialist to call.
```text
       /-> Search Specialist
Router --> Coding Specialist
       \-> Math Specialist
```
-   **Use Case:** Customer support (Billing vs Tech Support).
-   **Topology:** One node connects to many; paths diverge.

### 4. The Fan-In (Map-Reduce)
Multiple nodes run in parallel, and their results merge into one.
```text
Search 1 --\
Search 2 ---> Summarizer
Search 3 --/
```
-   **Use Case:** Researching a topic from 3 angles and combining results.

### 5. The Supervisor (Star Topology)
A central "Boss" node manages worker nodes.
```text
      /-- Coder --\
Boss <             > Boss
      \-- Tester -/
```
-   **Difference from Router:** The workers report *back* to the Boss (Cycle), whereas a Router sends them off to finish (DAG).

## Designing Topology

When building a graph, ask:
1.  **Width vs Depth:** Do I need parallel processing (Width/Fan-Out) or sequential reasoning (Depth/Chain)?
2.  **Centralization:** Do I want one LLM deciding everything (Supervisor), or do I want to hand off responsibility (Router)?

## Visualizing Topology

LangGraph Studio renders these topologies automatically. Viewing the shape often reveals bugs:
-   *detached clusters* (unreachable nodes).
-   *unintended cycles* (arrows pointing wrong way).

## Quick Summary

**1-Line Recall:** **Topology is the "skeleton" of the agent; common shapes include Chains (linear), Routers (divergent), and Supervisors (cyclic stars).**
