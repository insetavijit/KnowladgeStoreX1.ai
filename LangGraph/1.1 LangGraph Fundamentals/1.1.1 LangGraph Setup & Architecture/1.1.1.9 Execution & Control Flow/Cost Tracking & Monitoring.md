# Cost Tracking & Monitoring

**Core Definition:** Keeping track of how many tokens your agent is burning.

## Token Counting
This usually happens at the **LLM Node** level.
-   LangChain callbacks can aggregate token usage.
-   LangSmith automatically tracks robust cost metrics.

## Budgeting
To implement a "Budget":
1.  Add `total_cost` to your State schema.
2.  In every LLM node, parse `response.response_metadata["token_usage"]`.
3.  Update `total_cost` in the state.
4.  Add a Router edge: `if total_cost > LIMIT: return END`.

## Quick Summary

**1-Line Recall:** **Track costs by extracting token usage metadata from LLM responses and storing the running total in the graph state.**
