# Long-Running Workflows

## 1. Core Definition
**Long-Running Workflows** are processes that extend beyond the typical request-response timeout of a web server (e.g., seconds or minutes). These computations might take hours (deep research), days (waiting for user email response), or involve sporadic background processing.

## 2. Key Technical Details
*   **Persistence is Mandatory**: You cannot keep a long-running workflow in memory; if the server restarts, the state is lost. LangGraph's checkpointer mechanism saves the state to a database (Postgres, Redis) after every node execution.
*   **Resumption**: If a workflow pauses (for sleep or error) or the server crashes, it can be resumed from the last checkpoint using the `thread_id`.
*   **Async Background Jobs**: LangGraph is ideal for modeling "Async Agents" that receive a job, perform steps over time, and can be queried for status later.
*   **Failure Recovery**: If a node fails due to an API outage 4 hours into a job, you don't want to restart from minute 0. You want to replay from the failed node.

## 3. Mental Model
*   **Visual**: A save game file. You play level 1, save. Play level 2, save. If you turn off the console and come back next week, you load the save at level 2.
*   **Analogy**: sending a package via mail. You drop it off (Start). It goes to a sorting facility (Node A), sits there overnight (Persistence), gets on a truck (Node B), etc. Parameters exist (tracking ID) to identify the process over days.

## 4. Code Example (Persistence)
```python
# Just by adding a checkpointer, the graph becomes "Long-Running" capable
from langgraph.checkpoint.memory import MemorySaver # or PostgresSaver

checkpointer = MemorySaver()
app = workflow.compile(checkpointer=checkpointer)

# Run with a thread ID - this effectively creates a persistent session
config = {"configurable": {"thread_id": "job_123"}}
app.invoke(input_data, config)

# Later (even in a different process, if using DB checkpointer)
current_state = app.get_state(config)
```

## 5. One-Line Recall
For workflows spanning minutes to days, or across server restarts, LangGraph's native persistence (checkpointing) is the key enabler.
