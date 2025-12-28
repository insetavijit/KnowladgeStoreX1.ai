# Multi-Step Agents

## 1. Core Definition
**Multi-Step Agents** are systems where the LLM's workload is broken down into a sequence of distinct operations (or "reasoning steps") that must occur in a specific order. Unlike a simple chain, these agents often pass intermediate outputs between steps, accumulating context or refining a result. While linear sequences can be modeled as chains, "Agents" implies a degree of autonomy or complexity—often involving simple decision-making or error handling between steps.

## 2. Key Technical Details
*   **Sequential Logic**: Step B relies on the output of Step A.
*   **State Management**: As complexity grows, passing data purely through function arguments (as in chains) becomes unwieldy. LangGraph's shared state object makes it easier to manage context across multiple steps (e.g., `input` -> `plan` -> `draft` -> `critique` -> `final_output`).
*   **Error Handling**: If Step B fails, a multi-step agent might want to retry Step B or return to Step A, rather than crashing the whole pipe. This "non-linear" recovery is where LangGraph excels over simple chains.
*   **Observability**: Breaking a complex task into explicit graph nodes makes it easier to trace where the logic went wrong compared to a single massive prompt.

## 3. Mental Model
*   **Visual**: `[Plan Node] --> [Execute Node] --> [Verify Node]` (with potential loops back if Verification fails).
*   **Analogy**: An assembly line where a product moves from station to station. If a defect is found at station 3, it might be sent back to station 2 for rework.

## 4. Code Example (Linear vs Graph)
```python
# LangGraph allows capturing the intermediate state cleanly
class State(TypedDict):
    topic: str
    outline: str
    article: str

def generate_outline(state):
    # ... logic ...
    return {"outline": outline}

def write_article(state):
    # uses state["outline"]
    return {"article": article}

workflow = StateGraph(State)
workflow.add_node("outline", generate_outline)
workflow.add_node("write", write_article)
workflow.add_edge("outline", "write") # Explicit sequence
# Easy to add a "critique" loop here later
```

## 5. One-Line Recall
Multi-step agents benefit from LangGraph when the sequence needs state persistence, error recovery loops, or intermediate inspection.
