# Modular Node Design

## 1. Core Definition
**Modular Node Design** is the practice of keeping each node's logic focused, self-contained, and reusable. A well-designed node should perform a single logical unit of work (e.g., "fetch context," "generate draft," "parse output") rather than acting as a "god object" that tries to do everything in one massive function.

## 2. Key Technical Details
*   **Single Responsibility Principle (SRP)**: Each node should update a specific part of the state or perform a specific category of I/O.
*   **Pure Functions (Ideal)**: Where possible, design nodes as pure functions of the state (input state -> output state update) without hidden side effects. This makes unit testing trivial.
*   **Reusability**: If you implement a generic "summarize_text" node, it can be used in multiple places in the graph (or in different graphs) if it doesn't hardcode assumptions about the entire keyspace.
*   **Configuration**: Pass dynamic behavior via `configurable` params (part of the `config` argument in LangGraph) instead of hardcoding values inside the node.

## 3. Mental Model
*   **Visual**: LEGO blocks. Each block has a standard interface (studs) and a specific shape/color. You build a castle by snapping small, simple blocks together, not by molding one giant lump of clay.
*   **Analogy**: Unix tools (`grep`, `cat`, `awk`). Each does one thing well and accepts standard input/output streams. You pipe them together to build complex workflows.

## 4. Code Example (Monolithic vs Modular)

**Bad (Monolithic):**
```python
def god_node(state):
    # Does everything: search, parse, plan, write
    data = search(state["query"])
    if not data:
        return {"error": "no data"}
    plan = make_plan(data)
    draft = write(plan)
    return {"draft": draft} 
# Hard to test 'write' logic without mocking 'search'
```

**Good (Modular):**
```python
def search_node(state):
    return {"data": search(state["query"])}

def plan_node(state):
    return {"plan": make_plan(state["data"])}

def write_node(state):
    return {"draft": write(state["plan"])}
# Easy to unit test write_node separately
```

## 5. One-Line Recall
Design nodes as small, testable, single-purpose functions to keep the graph understandable and maintainable.
