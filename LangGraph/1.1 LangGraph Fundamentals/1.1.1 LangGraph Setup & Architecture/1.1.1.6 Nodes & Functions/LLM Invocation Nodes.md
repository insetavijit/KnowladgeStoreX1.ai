# LLM Invocation Nodes

**Core Definition:** Nodes that encapsulate the call to the Language Model. These are the "Brain" of the graph.

## The Standard Pattern

```python
async def call_model(state: State):
    messages = state["messages"]
    response = await model.ainvoke(messages)
    return {"messages": [response]}
```

## Key Responsibilities

1.  **Context Management:** Truncating old messages if the context window is full.
2.  **Prompt Binding:** Attaching system prompts that aren't in the state history.
3.  **Tool Binding:** Binding tools to the model *before* calling invoke.

```python
# Binding Tools
model_with_tools = model.bind_tools(tools)
response = await model_with_tools.ainvoke(messages)
```

## Streaming Output
If you want to stream tokens to the user, you don't change the node logic. You change how you *call* the graph (`graph.stream()`). Inside the node, you still use `.ainvoke()`.

*Advanced:* You *can* render tokens inside the node using callbacks or `astream_events` if you are building a custom UI.

## Quick Summary

**1-Line Recall:** **LLM Nodes wraps the model call; their job is to format the state into a prompt, invoke the model, and return the AIMessage.**
