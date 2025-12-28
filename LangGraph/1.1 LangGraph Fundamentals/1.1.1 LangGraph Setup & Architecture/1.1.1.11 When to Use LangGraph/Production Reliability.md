# Production Reliability

## 1. Core Definition
**Production Reliability** encompasses system stability, error handling, upgrades, and uptime. In the context of LLM agents, reliability often means "graceful failure" rather than 100% success (since LLMs are non-deterministic). LangGraph provides the control structures to ensure failures are handled predictably.

## 2. Key Technical Details
*   **Fault Tolerance**: You can wrap nodes in retry policies (standard Python decorators) or create explicit "Error Handler" nodes in the graph that trigger if a main node fails.
*   **Schema Validation**: By enforcing a state schema (Pydantic/TypedDict), LangGraph prevents "garbage in, garbage out" scenarios where a node passes malformed data downstream.
*   **Version Control**: Because the graph is defined in code, you can version control your agent logic. Rolling back a bad prompt is just a git revert.
*   **Timeouts & Safeguards**: You can enforce maximum iteration counts (`recursion_limit`) to prevent runaway costs/loops in production.

## 3. Mental Model
*   **Visual**: A safety net. The acrobat (Agent) might fall (Hallucinate/Fail), but the net (Graph Logic) catches them (Error Node) and puts them back on the platform (Retry) rather than letting them hit the ground (Crash).
*   **Analogy**: Industrial plumbing vs. a garden hose. A garden hose (Simple Chain) kinks and bursts. Industrial plumbing (LangGraph) has pressure valves, overflow tanks, and gauges to manage flow reliably.

## 4. Code Example (Recovery Path)
```python
def robust_scraper(state):
    try:
        # potentially flagon operation
        return scrape(state["url"])
    except Exception as e:
        # Return a flag to route to recovery
        return {"error": str(e)}

def route_error(state):
    if state.get("error"):
        return "fallback_search" # Graceful degradation
    return "summarize"

# The graph *guarantees* the fallback is called on error
workflow.add_conditional_edges("scraper", route_error, ...)
```

## 5. One-Line Recall
Use LangGraph to engineer reliability *around* the unreliable LLM, defining explicit recovery paths and safeguards.
