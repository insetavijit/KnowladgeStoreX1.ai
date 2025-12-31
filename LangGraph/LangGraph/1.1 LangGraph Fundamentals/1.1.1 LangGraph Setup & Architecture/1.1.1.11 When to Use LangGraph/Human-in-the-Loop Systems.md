# Human-in-the-Loop Systems

## 1. Core Definition
**Human-in-the-Loop (HITL)** systems are workflows that explicitly pause execution to wait for human intervention, approval, or feedback before proceeding. This is critical for sensitive actions (e.g., refunds, emails) or when the LLM encounters ambiguity it cannot resolve.

## 2. Key Technical Details
*   **Interrupts**: LangGraph supports `interrupt_before` and `interrupt_after` hooks on nodes. The graph suspends execution at these points.
*   **Persistence (Checkpoints)**: HITL *requires* a persistence layer. The state must be saved to a database (or memory) so it can wait indefinitely (minutes, days) for a human to resume it.
*   **State Modification**: Humans often don't just "approve"; they might edit the state (e.g., rewriting a draft email) before approving. LangGraph allows updating the thread state while it is interrupted.
*   **Routing**: The graph can branch based on human input (e.g., "Approve" -> Send, "Reject" -> Rewrite).

## 3. Mental Model
*   **Visual**: `[Draft Email Node] --|| PAUSE ||--> (Human Review) --> [Send Email Node]`.
*   **Analogy**: A driving instructor with a dual-brake car. The student (LLM) drives, but the instructor (Human) can pause the car, correct the steering, or take over completely if things look dangerous.

## 4. Code Example (Interrupt)
```python
# Compile with an interrupt on the 'action' node
app = workflow.compile(
    checkpointer=memory,
    interrupt_before=["send_payment"]
)

# Run until the interrupt
thread = {"configurable": {"thread_id": "1"}}
app.invoke(inputs, thread)

# ... System waits ... User reviews ...

# Resume execution (optionally updating state first)
app.invoke(None, thread) # Resumes from where it paused
```

## 5. One-Line Recall
LangGraph is essential for Human-in-the-Loop because its persistence and interrupt primitives allow workflows to pause, wait, and resume reliably.
