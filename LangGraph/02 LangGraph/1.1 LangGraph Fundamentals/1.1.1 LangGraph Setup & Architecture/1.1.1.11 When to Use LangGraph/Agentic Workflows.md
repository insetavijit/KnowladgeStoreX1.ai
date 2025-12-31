# Agentic Workflows

## 1. Core Definition
**Agentic Workflows** refer to systems where the "agent" is not just a single loop, but a composed architecture of multiple specialized agents or specific workflow patterns (like Planning, Reflection, Multi-Agent Collaboration). It moves beyond "one agent trying to do everything" to "a system of agents and rigid workflow steps collaborating."

## 2. Key Technical Details
*   **Cognitive Architectures**: Implementing patterns like **Plan-and-Solve**, **Reflection/Critique**, or **hierarchical teams**.
*   **Control Flow vs. Autonomy**: Agentic workflows blend *autonomy* (LLM decides within a node) with *engineering* (graph edges force a critique step after generation).
*   **Why LangGraph?**:
    *   **Orchestration**: You can hard-code the "workflow" steps (e.g., `Draft -> Critique -> Revise`) while letting the nodes use LLM intelligence.
    *   **Separation of Concerns**: Different nodes can use different prompts, different tools, or even different models (e.g., smart model for planning, fast model for expanding).
*   **Iterative Refinement**: These workflows almost always involve loops that improve output quality over time (creating a "flywheel" of quality).

## 3. Mental Model
*   **Visual**: A flowchart mixed with loops. `Planner -> Executor -> Reviewer`. If `Reviewer` rejects, arrow goes back to `Executor` or `Planner`.
*   **Analogy**: A newsroom. A Editor (Plan) assigns a Writer (Draft). The Writer submits to a Copy Editor (Critique). If bad, it goes back to Writer. If good, it goes to Publish. The workflow rules are rigid, but the content creation is creative (agentic).

## 4. Key Patterns
1.  **Reflection**: `Generate -> Critique -> Regenerate`.
2.  **Planning**: `Plan -> Execute Step 1 -> Execute Step 2 ...`.
3.  **Multi-Agent**: `Researcher` passes state to `Writer`.

## 5. One-Line Recall
Use LangGraph for Agentic Workflows to enforce structured collaboration (planning, offering critique) around LLM autonomy.
