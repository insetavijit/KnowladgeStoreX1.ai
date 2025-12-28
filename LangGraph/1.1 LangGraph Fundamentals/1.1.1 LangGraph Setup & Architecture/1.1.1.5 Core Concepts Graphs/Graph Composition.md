# Graph Composition

**Core Definition:** The ability to treat a compiled LangGraph application as a single Node inside *another* LangGraph application. This corresponds to **Subgraphs**.

**Why it Matters:** Real-world agents are too complex for one giant graph. You need to break them down.

## The Concept: "Turtles all the way down"

Every compiled graph implements the `Runnable` interface.
-   `Node` takes input, returns output.
-   `Graph` takes input, returns output.
-   Therefore, **Graph = Node**.

## How to Compose

### 1. Define Subgraph (Research Agent)
```python
research_workflow = StateGraph(ResearchState)
# ... add nodes ...
research_app = research_workflow.compile()
```

### 2. Define Supergraph (Main Agent)
```python
main_workflow = StateGraph(MainState)

# Add the subgraph as if it were a function
main_workflow.add_node("research_team", research_app)

main_workflow.add_edge(START, "research_team")
```

## State Management in Composition

The tricky part is passing state between the Parent and Child.
1.  **Shared Schema:** If Parent and Child use the exact same `TypedDict`, it flows automatically.
2.  **State Mapping:** If they differ, you need a "shim" function to translate.
    ```python
    def call_research(state: MainState):
        # Convert MainState -> ResearchState
        return research_app.invoke({"query": state["user_query"]})
    ```

## Benefits
1.  **Isolation:** The "Research Team" has its own internal state loops that the Main Agent doesn't care about.
2.  **Modularity:** Different teams can work on different subgraphs.

## Quick Summary

**1-Line Recall:** **Composition allows you to nest graphs inside graphs; treating a complex workflow as a single "black box" node.**
