# Memory Systems

**Core Definition:** **Memory** is the ability of an LLM application to persist context across multiple turns of conversation.

**The Shift:**
-   **LangChain (Legacy):** Memory was a separate class (`ConversationBufferMemory`) that you "attached" to a chain. It magically updated itself.
-   **LangGraph (Modern):** **State IS Memory.** There is no separate memory class. The list of messages in your `GraphState` *is* the memory.

## Legacy Memory Types (For reference)
You might see these in older docs:
-   **`ConversationBufferMemory`**: Stores all messages raw.
-   **`ConversationSummaryMemory`**: Periodically summarizes old messages to save tokens.
-   **`EntityMemory`**: Extracts facts about entities (people, places) and stores them.

## The LangGraph Approach: "State Persistence"

In LangGraph, we don't use the memory classes. Instead, we use **Checkpointers**.

1.  **Short-term Memory (The State):**
    -   Defined in your schema (e.g., `messages: list`).
    -   As the graph runs, nodes append to this list.
    -   When the graph finishes, the state holds the full conversation for that run.

2.  **Long-term Persistence (Checkpointers):**
    -   To remember things *between* user interactions (e.g., waiting for user input), we pass a `checkpointer` (like `MemorySaver` or `SqliteSaver`) when compiling the graph.
    -   `graph = builder.compile(checkpointer=memory)`

### Benefits of State-as-Memory
-   **Explicit:** No magic background updates. If you want to summarize memory, you add a "Summarize Node" to your graph.
-   **Control:** You decide exactly what gets saved and what gets discarded.

## Quick Summary

**1-Line Recall:** **We don't use "Memory Classes" in LangGraph; we use the Graph State for context and Checkpointers for persistence.**
