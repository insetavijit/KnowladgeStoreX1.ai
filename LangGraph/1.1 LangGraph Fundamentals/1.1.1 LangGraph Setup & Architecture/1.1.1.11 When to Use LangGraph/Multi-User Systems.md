# Multi-User Systems

## 1. Core Definition
**Multi-User Systems** are applications where a single graph definition serves many concurrent users, each with their own isolated conversation history and state. LangGraph handles this concurrency via **Thread-Level Isolation**.

## 2. Key Technical Details
*   **Thread ID**: The primary key for state isolation. `{"configurable": {"thread_id": "user_42_session_9"}}`.
*   **Shared Definition, Independent State**: You define the graph *topology* once (`workflow = StateGraph(...)`). You compile it once (`app = workflow.compile()`). But you invoke it thousands of times with different `thread_id`s. Each invocation instantiates a unique state trajectory.
*   **Race Conditions**: LangGraph leverages the database's locking (via checkpointers) to handle race conditions if the *same* thread is accessed rapidly, but different threads are totally independent.
*   **Scalability**: Since valid agent state is stored in the DB (not Python memory), the API servers can be stateless and horizontally scaled. Any server can pick up any user's request by looking up the `thread_id`.

## 3. Mental Model
*   **Visual**: A hotel (The Graph Definition). It has many identical rooms (Threads). Guest A is in Room 101. Guest B is in Room 102. They use the same layout (furniture/amenities), but Guest A's mess doesn't appear in Guest B's room.
*   **Analogy**: A web browser. The code (Chrome) is the same, but Tab A (User 1) is on Google, and Tab B (User 2) is on Wikipedia. They don't interfere.

## 4. Code Example (Multi-Tenancy)
```python
# Same app object
app = workflow.compile(checkpointer=PostgresSaver(...))

# User A Request
app.invoke({"messages": ["Hi"]}, {"configurable": {"thread_id": "user_A"}})

# User B Request (Totally separate memory)
app.invoke({"messages": ["Hello"]}, {"configurable": {"thread_id": "user_B"}})
```

## 5. One-Line Recall
Use LangGraph's `thread_id` mechanism to effortlessly manage state for millions of concurrent users with a single graph definition.
