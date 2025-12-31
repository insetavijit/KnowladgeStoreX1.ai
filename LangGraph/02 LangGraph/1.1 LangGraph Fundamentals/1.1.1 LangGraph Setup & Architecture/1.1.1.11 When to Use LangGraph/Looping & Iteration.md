# Looping & Iteration

## 1. Core Definition
**Looping & Iteration** involve repeating a specific set of operations until a condition is met (e.g., "Keep improving the summary until the critique score is > 8/10"). This is the "Cycle" in "Directed Cyclic Graph" and is the primary differentiator between LangGraph and simpler DAG (Directed Acyclic Graph) frameworks.

## 2. Key Technical Details
*   **Cycles**: An edge that points from a downstream node back to an upstream node.
*   **Convergence**: The system assumes the state evolves with each loop (e.g., the draft gets better), eventually satisfying an exit condition.
*   **Recursion Limit**: To prevent infinite loops (cost/safety), LangGraph enforces a `recursion_limit` (default 25) which raises an error if the graph cycles too many times.
*   **Accumulation**: Looping often requires a state schema that handles accumulation (e.g., appending messages to a list) rather than just overwriting, so the context of previous attempts isn't lost.

## 3. Mental Model
*   **Visual**: A circular arrow. `Generate -> Critique -> (if bad) -> Generate`.
*   **Analogy**: Polishing a shoe. You apply polish, buff it, check the shine. If it's not shiny enough, you apply polish and buff again. You repeat the *same steps* but the *state* (shininess) changes.

## 4. Code Example (The Cycle)
```python
# A simple improve loop
def critique_node(state):
    score = score_model.invoke(state["draft"])
    return {"score": score}

def should_continue(state):
    if state["score"] > 8:
        return "end" # Goes to END
    return "revise" # Loops back

workflow.add_edge("generate", "critique")
workflow.add_conditional_edges(
    "critique",
    should_continue,
    {
        "end": END,
        "revise": "generate" # The Loop
    }
)
```

## 5. One-Line Recall
LangGraph is the correct tool whenever you need to retry, refine, or repeat steps based on dynamic feedback (loops).
