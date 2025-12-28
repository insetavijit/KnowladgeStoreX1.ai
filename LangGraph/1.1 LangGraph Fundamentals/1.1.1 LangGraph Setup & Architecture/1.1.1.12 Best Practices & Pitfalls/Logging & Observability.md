# Logging & Observability

## 1. Core Definition
**Logging & Observability** refers to instrumenting the graph to emit signals about its internal operation—not just "it worked" or "it failed," but "how it behaved." For complex graphs, this means tracking node transitions, LLM tokens, tool inputs/outputs, and latency per step.

## 2. Key Technical Details
*   **LangCode/LangSmith**: The primary observability tool for LangGraph. It automatically visualizes the graph execution, showing input/output for every node.
*   **Structured Logging**: Use structured logs (JSON) over print statements. Log key events: `GraphStart`, `NodeEnter`, `NodeExit`, `ToolCall`, `GraphEnd`.
*   **Correlation IDs**: Ensure every log line carries the `thread_id` and `run_id` so you can stick together logs from a single user session across distributed logs (e.g., in Datadog or CloudWatch).
*   **Sanitization**: Be careful not to log PII (Personal Identifiable Information) or API keys. Implement log redaction filters.

## 3. Mental Model
*   **Visual**: X-Ray Vision. Without observability, the agent is a black box. With it, you see the skeleton (graph structure) and the blood flow (data) in real-time.
*   **Analogy**: Dashboard in a cockpit. You have gauges for fuel, altitude, speed, and engine temp. You don't fly the plane by just looking out the window (output); you scan the instruments (observability) to ensure health.

## 4. One-Line Recall
Instrument everything; in production, you cannot fix what you cannot see.
