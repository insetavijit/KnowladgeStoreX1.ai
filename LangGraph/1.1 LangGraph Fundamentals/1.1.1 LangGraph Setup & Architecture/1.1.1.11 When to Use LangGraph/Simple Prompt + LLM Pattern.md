# Simple Prompt + LLM Pattern

## 1. Core Definition
The **Simple Prompt + LLM Pattern** represents the most basic interaction with a Large Language Model: a single request-response cycle. It involves taking an input, inserting it into a prompt template, sending it to the LLM, and parsing the string output. In this pattern, there is no state persistence, no looping, and no complex branching. It is essentially a stateless function call wrapping an LLM capability.

## 2. Key Technical Details
*   **Statelessness**: Each invocation is independent. The system retains no memory of previous interactions unless manually fed back as context in a new request (managed externally, not by the "graph").
*   **Latency**: Typically offers the lowest latency as there is only one model round-trip.
*   **Implementation**: Can be implemented with a simple HTTP client or basic LangChain `LLMChain` (or LCEL `prompt | llm | parser`).
*   **LangGraph Applicability**: generally **NOT** a candidate for LangGraph. Using a graph for a single linear step introduces unnecessary overhead (setup, state schema, checkpointing) without providing benefits.
*   **Exceptions**: You might allow a "simple prompt" node within a larger graph if it's just one step in a complex workflow (e.g., a "Summarize" node at the end of a research agent).

## 3. Mental Model
*   **Visual**: Input --> [Prompt Template] --> [LLM] --> Output
*   **Analogy**: Asking a question to a stranger on the street. You ask, they answer, you part ways. There is no ongoing relationship or memory.

## 4. Code Example (Comparison)
**Without LangGraph (Recommended):**
```python
# Simple LCEL chain
chain = prompt | model | parser
result = chain.invoke({"input": "Hello"})
```

**With LangGraph (Overkill):**
```python
# Unnecessary complexity for a single step
def simple_node(state):
    return {"messages": [model.invoke(state["messages"])]}

graph = StateGraph(MessagesState)
graph.add_node("call_llm", simple_node)
graph.add_edge(START, "call_llm")
graph.add_edge("call_llm", END)
app = graph.compile()
```

## 5. One-Line Recall
For single-step, stateless LLM calls, use simple chains or API calls; avoid graph overhead.
