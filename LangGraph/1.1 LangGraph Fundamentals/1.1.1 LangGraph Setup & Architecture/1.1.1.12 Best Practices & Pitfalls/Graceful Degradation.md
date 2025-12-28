# Graceful Degradation

## 1. Core Definition
**Graceful Degradation** is the system's ability to maintain partial functionality when tailored components fail. If the primary "Smart LLM" is down or timed out, the system should fall back to a "Dumb Heuristic" or "Cached Response" rather than throwing a 500 Error.

## 2. Key Technical Details
*   **Fallback Nodes**: Nodes designed to run only if the primary node fails (caught via `conditional_edges` on error state).
*   **Model Fallback**: If GPT-4 is overloaded, fall back to GPT-3.5-Turbo or Claude-Instant.
*   **Default Responses**: "I'm having trouble thinking right now, but here are some search results" is better than a blank screen.
*   **Circuit Breakers**: If a tool fails 5 times in a row, stop calling it for 5 minutes and tell the user "Tool unavailable" immediately.

## 3. Mental Model
*   **Visual**: Escalator becoming stairs. An escalator that breaks doesn't become a wall; it becomes stairs. It's slower and harder to use, but you can still get to the next floor.
*   **Analogy**: Run-flat tires. If you get a puncture, you can still drive at 50mph to get home. You aren't stranded.

## 4. One-Line Recall
Design paths for failure so your agent can fail *partially* (degrade) rather than completely (crash).
