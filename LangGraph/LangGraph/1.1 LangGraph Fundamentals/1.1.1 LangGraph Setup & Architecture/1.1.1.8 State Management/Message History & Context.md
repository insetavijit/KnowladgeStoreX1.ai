# Message History & Context

**Core Definition:** The most crucial part of State for Chatbots—the list of messages.

## Using `Annotated` for Append Logic
Almost every LangGraph agent starts with:

```python
from typing import Annotated
from langgraph.graph.message import add_messages

class State(TypedDict):
    messages: Annotated[list, add_messages]
```

## `add_messages` Reducer
This built-in reducer is smart.
1.  **Appends** new messages to the list.
2.  **Updates** existing messages if IDs match (allows editing old messages!).
3.  **Handles** turning a single message into a list.

## Usage in Nodes
Nodes just return the *new* message(s).

```python
def bot_node(state):
    return {"messages": [AIMessage(content="Hello")]}
```

## Context Window Management
The history grows forever. You need to manage it.
-   **Summarization:** A node that reads 50 messages and replaces them with 1 summary message.
-   **Filtering:** Passing only the last N messages to the LLM (even if State keeps all of them).

## Quick Summary

**1-Line Recall:** **Use `Annotated[list, add_messages]` to automatically handle appending conversation history; it is the backbone of memory in LangGraph.**
