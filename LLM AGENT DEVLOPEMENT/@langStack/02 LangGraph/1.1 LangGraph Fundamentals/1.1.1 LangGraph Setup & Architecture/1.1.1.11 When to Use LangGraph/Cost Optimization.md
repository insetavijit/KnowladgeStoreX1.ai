# Cost Optimization

## 1. Core Definition
**Cost Optimization** involves designing the system to minimize token usage and API calls. While LangGraph itself adds no runtime cost, its control flow capabilities allow for sophisticated optimization strategies that are hard to implement in simple chains.

## 2. Key Technical Details
*   **Conditional Execution**: Don't run the expensive "Deep Analysis" node if the "Triage" node says the query is simple. LangGraph makes skipping steps explicit and easy.
*   **Caching/Memoization**: You can implement caching nodes that check a DB before calling the LLM.
*   **Earlier Termination**: Through `conditional_edges`, the agent can decide to stop early if it finds the answer, saving distinct steps compared to a fixed "5-step chain."
*   **Smaller Models**: You can route simple tasks to cheaper/faster models (e.g., GPT-3.5) and reserve powerful models (GPT-4) only for the complex "Reasoning" nodes.

## 3. Mental Model
*   **Visual**: A train track switch. The express train (Expensive) goes one way, the slow freight train (Cheap) goes another. You control the switch.
*   **Analogy**: Hiring contractors. You don't hire a Senior Architect to dig a ditch. You hire a Ditch Digger (Cheap Node). You hire the Architect (Expensive Node) only for the blueprints. LangGraph is the HR manager assigning the right task to the right resource.

## 4. Code Example (Model Routing)
```python
def triage_node(state):
    # Cheap classification
    topic = fast_model.invoke(state["query"])
    return {"topic": topic}

def router(state):
    if state["topic"] == "complex_physics":
        return "gpt4_node"
    return "gpt35_node"

# Optimizes cost by default
workflow.add_conditional_edges("triage", router, ...)
```

## 5. One-Line Recall
Explicit control flow allows fine-grained routing to cheaper models or skipping unnecessary steps, significantly reducing API bills.
