# Resource Limits & Quotas

## 1. Core Definition
**Resource Limits & Quotas** defend the system (and wallet) against runaway agents. This involves setting hard caps on tokens, steps, execution time, and tool calls per workflow run.

## 2. Key Technical Details
*   **Recursion Limit**: The hard cap on graph steps (primary defense).
*   **Timeouts**: Set execution timeouts (e.g., `run_tree(..., timeout=60s)`). If an agent hangs on a network call, kill it.
*   **Token Budgets**: If possible, track accumulated tokens in the state and `return END` if the budget (e.g., $1.00) is exceeded.
*   **Rate Limiting**: Use external limiters (Redis/TokenBucket) to ensure one user cannot launch 1000 concurrent graph runs.

## 3. Mental Model
*   **Visual**: Fuse Box. If a device draws too much power, the fuse breaks immediately to prevent the house from burning down.
*   **Analogy**: Prepaid Phone Card. You can talk as long as you have minutes. When minutes hit 0, the call cuts. It prevents specific surprise bills.

## 4. One-Line Recall
Enforce limits at every layer (time, steps, tokens) to ensure an error or attack doesn't drain unlimited resources.
