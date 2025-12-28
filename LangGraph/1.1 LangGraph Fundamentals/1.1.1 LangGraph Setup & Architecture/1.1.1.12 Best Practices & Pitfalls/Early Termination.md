# Early Termination

## 1. Core Definition
**Early Termination** is the efficiency practice of ending a workflow as soon as the goal is met, rather than forcing the agent to complete a fixed number of steps. This improves latency and reduces costs.

## 2. Key Technical Details
*   **Success Conditions**: Define clear criteria for "Done" (e.g., "Answer found", "Confidence > 0.9").
*   **Conditional Edges**: Check these conditions after every major step. `Step A -> (Done?) -> End` OR `Step A -> Step B`.
*   **Avoid Fixed Chains**: Do not build `A -> B -> C -> D` if `D` is sometimes redundant. Use a graph where `A` can jump straight to `END`.
*   **User Interrupt**: Allow users to manually signal "Stop/Cancel" which triggers an immediate transition to END (handled via interrupts or cancellation tokens).

## 3. Mental Model
*   **Visual**: An express elevator. It stops at your floor and opens the doors. It doesn't force you to go to the roof and back down before letting you out.
*   **Analogy**: Searching for keys. Once you find them in the kitchen, you stop searching. You don't proceed to search the bedroom and basement "just to be sure" (unless you are very anxious/thorough, which costs time).

## 4. Code Example
```python
def check_goal(state):
    if is_valid_answer(state["answer"]):
        return END # Early exit
    return "next_reasoning_step"

workflow.add_conditional_edges("search", check_goal)
```

## 5. One-Line Recall
Always provide an "off-ramp" (conditional edge to END) after expensive steps to exit as soon as success is achieved.
