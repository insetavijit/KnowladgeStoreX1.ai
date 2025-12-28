# Serialization & LCEL

**Core Definition:** **LCEL (LangChain Expression Language)** is the declarative way to compose chains. **Serialization** is the ability to save these chains (and their states) to disk and reload them later.

**Why it matters:** LangGraph's nodes are often built using LCEL chains because they are concise, support streaming out-of-the-box, and are easy to inspect.

## LCEL: The Pipe Syntax (`|`)

LCEL unifies invocation, batching, and streaming.
```python
# The "Unix Pipe" for AI
chain = prompt | model | parser
```

**Why use it in LangGraph?**
-   **Reliability:** LCEL chains automatically handle async and streaming. A node built with LCEL is "well-behaved" by default.
-   **Parallelism:** `RunnableParallel` allows a node to do two things at once (e.g., fetch context AND format history).

## Serialization

How do you save an agent?
1.  **Code as Source:** The best way to "save" a graph definition is to keep the Python code versioned (git).
2.  **State Serialization:** LangGraph automatically serializes the *state* (the checkpointer uses `pickle` or JSON) so you can pause/resume.
3.  **Component Serialization:**
    -   `dumpd(runnable)`: Dumps a runnable to a JSON-serializable dict.
    -   `load(path)`: Loads it back.
    -   *Note: This is less common now; code-based definition is preferred.*

## LangGraph is declarative
Just like LCEL is declarative ("Do step A, then B"), LangGraph is declarative ("Node A goes to Node B").
-   This declarative nature is what allows **LangStudio** (the GUI) to visualize your graph. It's not just running code; it's a structure the system understands.

## Quick Summary

**1-Line Recall:** **LCEL uses pipes (`|`) to compose logic declaratively, which makes LangGraph nodes concise and compliant with streaming standards.**
