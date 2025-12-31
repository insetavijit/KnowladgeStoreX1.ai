# Multi-Turn Conversations

**Core Definition:** Remembering what happened 5 minutes ago.

## Chains: List Appending
You have to manually manage a `chat_history` list outside the chain, and pass it in every time.
`chain.invoke({"question": "Hi", "history": history_list})`

## Graphs: Native State
The graph *is* the history.
-   **Schema:** `messages: Annotated[list, add_messages]`
-   **Execution:** `output = graph.invoke(input)` automatically updates the persistent state.
-   **Next Turn:** Just call `graph.invoke` again with the *new* user message. You don't need to re-send the history.

## Quick Summary

**1-Line Recall:** **LangGraph handles multi-turn conversation state natively; Chains require the developer to manually manage and inject history on every call.**
