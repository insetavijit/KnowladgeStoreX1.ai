# Graph Theory Fundamentals

**Core Definition:** At its heart, **LangGraph** is an implementation of a mathematical structure called a **Graph**. A graph is simply a set of objects (nodes) where some pairs of objects are connected by links (edges).

**Why This Matters:**
To master LangGraph, you don't need a PhD in math, but you need to think in terms of **topology** (shape) rather than **linear sequences**. Standard coding is often linear (line 1, then line 2). Agents are non-linear (Loop until X, then maybe go to Y or Z).

## Key Components in Theory vs. LangGraph

| Graph Theory Term | LangGraph Equivalent | Function |
| :--- | :--- | :--- |
| **Vertex / Node** | `Node` | A step where computation happens (LLM call, Tool execution). |
| **Directed Edge** | `Edge` / `ConditionalEdge` | A one-way street from Node A to Node B. |
| **State** | `GraphState` | The "token" or data packet that travels along the wires. |
| **Walk / Path** | Execution Trace | The specific sequence of nodes visited in a single run. |
| **Cycle** | Loop | A path that starts and ends at the same node (e.g., `model -> tool -> model`). |

## The Type of Graph: Directed State Graph

LangGraph uses a specific flavor of graph:
1.  **Directed:** Edges have arrows. You go from A to B, not back again (unless explicitly wired).
2.  **Stateful:** The "walker" on the graph carries a backpack of data (the State) that gets modified at each stop.

## Visualizing Control Flow

In traditional code:
```python
# Linear Control Flow
result = step_1()
if check(result):
    step_2()
else:
    step_3()
```

In Graph Logic:
-   **Nodes**: `step_1`, `step_2`, `step_3`.
-   **Conditional Edge**: A router function attached to `step_1` that points to either `step_2` or `step_3`.

## Graph Traversals

When you "invoke" a graph, the runtime performs a **Traversal**:
1.  Start at `START` node.
2.  Follow the edge.
3.  Run the Node.
4.  Update State.
5.  Check for next edge.
6.  Repeat until `END` node is reached.

## Deep Dive: Connectivity

-   **Reachable:** A node is "reachable" if there is a path from START to it.
-   **Dead End (Sink):** A node with no outgoing edges. In LangGraph, this is an error (unless it is the `END` node).
-   **Source:** A node with no incoming edges (usually `START`).

## Quick Summary

**1-Line Recall:** **LangGraph maps "Code Execution" to "Graph Traversal," where Nodes are functions and Edges are the logic for what function runs next.**
