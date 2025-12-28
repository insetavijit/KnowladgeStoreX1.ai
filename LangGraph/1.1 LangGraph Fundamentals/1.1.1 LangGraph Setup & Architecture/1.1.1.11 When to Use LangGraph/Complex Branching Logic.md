# Complex Branching Logic

## 1. Core Definition
**Complex Branching Logic** refers to workflows where the path of execution isn't a straight line but splits into multiple possibilities based on dynamic criteria. While simple `if/else` can be handled in a chain, LangGraph is needed when these branches lead to entirely different sub-graphs, loops, or when the decision logic itself requires an LLM call.

## 2. Key Technical Details
*   **Conditional Edges**: The primary primitive for branching. You define a "router" function that inspects the state and returns the name of the next node (e.g., `should_continue` -> "next_step" or "end").
*   **Dynamic Decision Handling**: The decision isn't just A or B; it could be A, B, C, or Loop back to A.
*   **Parallel Branching (Fan-out)**: LangGraph supports splitting execution into multiple parallel nodes (e.g., "Research Topic A" and "Research Topic B" running simultaneously) and merging them back.
*   **State-Dependent Routing**: Routing decisions can be based on accumulating history, not just the last output (e.g., "If we've tried 3 times, stop").

## 3. Mental Model
*   **Visual**: A decision diamond in a flowchart. One arrow in, multiple labeled arrows out.
*   **Analogy**: A Choose Your Own Adventure book. At the bottom of the page, you make a choice ("Turn to page 45" or "Turn to page 88"). The story structure is the graph; your choices are the conditional edges.

## 4. Code Example (Conditional Routing)
```python
def router(state):
    # Logic can be simple rule or complex LLM classification
    if "error" in state:
        return "handle_error"
    elif state["score"] > 0.8:
        return "publish"
    else:
        return "revise"

# The classic conditional edge setup
workflow.add_conditional_edges(
    "review_node",  # Source node
    router,         # Routing function
    {               # Map return value to Node Name
        "handle_error": "error_handler",
        "publish": END,
        "revise": "editor"
    }
)
```

## 5. One-Line Recall
Use LangGraph when your workflow needs to dynamically choose between multiple distinct downstream paths or execute parallel branches.
