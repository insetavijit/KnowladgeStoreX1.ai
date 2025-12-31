# Graphs with Cycles

**Core Definition:** A graph containing at least one path that starts at a node and eventually returns to that same node. This is the **structural definition of an Agent**.

**The Loop:**
`Model -> Tools -> Model`
This simple cycle is what separates a "Script" from an "Agent".

## Why Cycles? (The Cognitive Loop)

Real problem-solving is iterative.
-   **Humans:** We write code -> run it -> see error -> fix code -> run it again.
-   **Agents:** Need the same ability to **backtrack** and **retry**.

### Common Cyclic Patterns

1.  **The ReAct Loop:**
    -   *Think:* "I need to check the weather."
    -   *Act:* Call WeatherTool.
    -   *Observe:* "It's raining."
    -   *loop back to Think:* "Okay, I should bring an umbrella."

2.  **The Self-Correction Loop:**
    -   *Generate:* Write Python code.
    -   *Test:* Run unit test.
    -   *Conditional:* If Fail -> **Loop back** to Generate with error msg. If Pass -> End.

3.  **The Human-in-the-Loop:**
    -   *Execute:* Propose email.
    -   *Wait:* Ask Human.
    -   *Correction:* Human says "Change tone".
    -   *Loop back:* Rewrite email.

## Managing Infinite Loops

Cycles introduce a danger: **Infinite Recursion**.
If the model keeps deciding to call the tool, the graph runs forever.

### LangGraph Safeguards

1.  **`recursion_limit`:**
    LangGraph enforces a hard limit (default 25 steps) on how many nodes can be visited in a single run.
    ```python
    graph.invoke(inputs, config={"recursion_limit": 50})
    ```
    *If the limit is hit, it raises a `RecursionLimitError`.*

2.  **Termination Conditions:**
    You must design your graph logic to *converge*.
    -   *Logic:* "If retry_count > 3, go to END."

## State Evolution in Cycles

In a cycle, the State **must change**.
-   If `State` is identical to the last time we visited Node A, we are in a deterministic infinite loop.
-   Usually, the `messages` list grows (adding the tool output), which gives the model new information to break the loop.

## Quick Summary

**1-Line Recall:** **Cycles allow Agents to iterate, correct errors, and reason over time; they require `recursion_limits` to prevent infinite execution.**
