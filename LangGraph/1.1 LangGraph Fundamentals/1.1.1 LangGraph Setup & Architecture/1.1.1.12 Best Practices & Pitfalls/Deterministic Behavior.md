# Deterministic Behavior

## 1. Core Definition
**Deterministic Behavior** means that given the same input `X` and the same starting state `S`, the graph always produces result `Y`. While LLMs are inherently non-deterministic (unless temperature=0), the *routing logic* and *state updates* of your graph should be strictly deterministic to make debugging possible.

## 2. Key Technical Details
*   **Temperature=0**: For logic/routing nodes, always use low or zero temperature.
*   **Seeding**: Some models support seed parameters to force reproducibility.
*   **Logic Determinism**: Ensure Python logic (routers) doesn't rely on random numbers (`random.choice`) or external changing state (current time) unless absolutely necessary and mocked in tests.
*   **State-Only dependency**: Routing decisions should depend *only* on the State, not on global variables or external DBs that might change mid-run.

## 3. Mental Model
*   **Visual**: A math equation. `2 + 2` is always `4`. If it's sometimes `5` (Non-deterministic), you can't build a bridge (Production App) with it.
*   **Analogy**: DVD vs Live TV. A DVD (Deterministic) plays the exact same movie every time you press play. Live TV (Non-deterministic) changes every time. You want your code to be a DVD.

## 4. One-Line Recall
Maximize determinism in code and routing; isolate non-determinism strictly to the LLM generation step.
