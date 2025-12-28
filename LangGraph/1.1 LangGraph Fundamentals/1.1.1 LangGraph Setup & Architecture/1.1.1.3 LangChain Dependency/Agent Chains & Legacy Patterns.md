# Agent Chains & Legacy Patterns

**Core Definition:** "Legacy" refers to the older, pre-LangGraph ways of building agents in LangChain, specifically the **`AgentExecutor`** and linear `Chain` classes.

**Why Study This:** You will encounter older codebases or tutorials using `initialize_agent` or `AgentExecutor`. Understanding why LangGraph replaced them is key to your architectural decisions.

## The Old Way: AgentExecutor

`AgentExecutor` was a "black box" runtime loop.
-   **How it worked:** You gave it tools and an LLM, and it ran a hardcoded `while` loop (Thought -> Action -> Observation) until it finished.
-   **The Problem:** Customizing the loop was incredibly hard. Adding a "human approval step" or "retry logic" required monkey-patching the class.

## The New Way: LangGraph

LangGraph "explodes" the `AgentExecutor` black box into visible nodes.
-   **ReAct Pattern:** Instead of a hidden loop, you explicitly draw the graph:
    `Model -> ToolNode -> Model`.
-   **Benefit:** You can insert a node *anywhere*. Want a "Check for Hallucinations" step after the model runs? Just draw an edge to it.

## Legacy Chains to Know

1.  **`LLMChain`**: The primitive "Prompt + LLM". Superseded by `prompt | llm` (LCEL).
2.  **`ConversationalRetrievalChain`**: A monolithic class for RAG. Superseded by explicit RAG graphs.
3.  **`RouterChain`**: A primitive for routing. Superseded by LangGraph "Conditional Edges".

## Migration Strategy

If you see:
```python
# Legacy
agent = initialize_agent(tools, llm, agent=AgentType.OPENAI_FUNCTIONS)
agent.run("input")
```

Think:
```python
# Modern LangGraph
graph = create_react_agent(llm, tools)
graph.invoke({"messages": [("human", "input")]})
```
*Note: `create_react_agent` is a high-level helper in LangGraph that mimics the old `AgentExecutor` ease-of-use but keeps the graph structure underneath.*

## Quick Summary

**1-Line Recall:** **AgentExecutor was a hardcoded loop; LangGraph is a customizable loop. We move from "Configuring the black box" to "Drawing the flow".**
