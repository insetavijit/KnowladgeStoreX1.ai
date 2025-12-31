# Performance & Routing Efficiency

**Core Definition:** Optimizing edges to minimize latency and token usage.

## 1. Fast Pathing (The "Happy Path")
Design your graph so the most common scenario takes the fewest steps.
-   *Inefficient:* `Start -> Generic_Analyze -> Router -> Simple_Task`
-   *Efficient:* `Start -> (Conditional: Is Simple?) -> Simple_Task`

## 2. Avoid "Thinking" Routers
If a router needs to call an LLM ("Should I do X?"), that adds latency/cost.
-   **Optimization:** Can you use a keyword match or regex instead?
-   *Example:* If user says "Help", route to Support immediately (0ms) instead of asking GPT "Is this a support request?" (800ms).

## 3. Pruning Branches
In conditional fan-out, don't return branches you don't use.
-   If you start 5 parallel searches, you pay for 5 API calls.
-   Better: Use a limiter to pick the top 3 likely needed.

## 4. Caching Routing Decisions
If the user asks the same question twice, memoize the router output.

## Quick Summary

**1-Line Recall:** **The fastest router is a regex; avoid using LLMs for routing if simple heuristics can handle 80% of the traffic.**
