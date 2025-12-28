# Monitoring Production Graphs

## 1. Core Definition
**Monitoring Production Graphs** shifts focus from "debugging code" to "observing health." It involves tracking metrics like Success Rate, Average Latency per Node, Cost per Run, and identifying "Black Hole" nodes (nodes where users frequently drop off).

## 2. Key Technical Details
*   **Success vs Failure**: distinct terminal states. Track how many runs hit `END` vs `ERROR`.
*   **Latency Heatmap**: Which node is the bottleneck? (Usually the LLM or a slow Tool).
*   **Verbatim Sampling**: Randomly review 1% of traces to check qualitative performance (Human Evaluation).
*   **Alerting**: Alert if `Error Rate > 5%` or `Avg Duration > 30s`.

## 3. Mental Model
*   **Visual**: Air Traffic Control. You monitor hundreds of flights (Agents). You don't care about the drink service on Flight 101 unless it sends a distress signal. You care about collisions and delayed landings.
*   **Analogy**: Vital Signs Monitor. Heart rate (Latency), Blood Pressure (Error Rate), Oxygen (Success Rate).

## 4. One-Line Recall
Move beyond "viewing traces" to "tracking metrics" to understand the aggregate health of your deployed agents.
