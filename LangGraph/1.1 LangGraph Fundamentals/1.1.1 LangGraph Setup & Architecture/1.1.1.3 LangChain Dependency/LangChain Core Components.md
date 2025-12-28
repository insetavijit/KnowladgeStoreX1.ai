# LangChain Core Components

**Core Definition:** **LangChain** provides the standard building blocks (primitives) for building LLM applications. LangGraph uses these components as the "work units" inside its nodes.

**Position in Ecosystem:**
LangGraph orchestrates the *flow*, while LangChain Core provides the *capabilities* (calling models, formatting strings, parsing outputs).

## Key Components

### 1. Models (LLMs & Chat Models)
The computational engines.
-   **`BaseLLM`**: For pure text-in/text-out models (legacy or completion-based).
-   **`BaseChatModel`**: For message-based models (System/Human/AI).
-   **LangGraph Usage**: You typically invoke limited `ChatModel` calls inside a node to generate the next state update.

### 2. Prompts
Templates to structure inputs for models.
-   **`PromptTemplate`**: String substitution (f-string/jinja2).
-   **`ChatPromptTemplate`**: Structured lists of messages (System, Human, AI, Placeholders).
-   **LangGraph Usage**: Nodes usually format state data into a `ChatPromptTemplate` before passing it to the model.

### 3. Output Parsers
Extracts structured data from model text.
-   **`StrOutputParser`**: Returns the raw string.
-   **`JsonOutputParser`**: Extracts and validates JSON.
-   **`PydanticOutputParser`**: Validates output against a Pydantic object.
-   **LangGraph Usage**: Parsers ensure the model's output is clean before it updates the graph state.

### 4. Tools
Functions that models can call.
-   **`BaseTool`**: The interface for all tools (name, description, args schema).
-   **`@tool`**: Decorator to turn Python functions into tools.
-   **LangGraph Usage**: Tools are the primary way agents interact with the world. A "Tool Node" in LangGraph executes these tools.

### 5. Runnables (LCEL)
The protocol that binds everything together.
-   **Unified Interface**: Every component (Model, Prompt, Parser, Chain) implements `Runnable`.
-   **Methods**: `.invoke()`, `.stream()`, `.batch()`.
-   **Composition**: `prompt | model | parser`.
-   **LangGraph Usage**: Nodes often consist of an LCEL chain: `chain = prompt | model`.

### 6. Retrievers (RAG)
Interfaces for fetching external data.
-   **`VectorStoreRetriever`**: Fetches from semantic search.
-   **`WebLoader`**: Fetches from URLs.
-   **LangGraph Usage**: A "Retrieval Node" might look up context to populate the state before the model runs.

## Relationship to LangGraph

Think of **LangChain** as the **bricks** and **LangGraph** as the **blueprint**.

| LangChain Component | Role in LangGraph |
| :--- | :--- |
| **Prompt** | Formats the `GraphState` for the LLM. |
| **Model** | Performs the reasoning step in a Node. |
| **Tool** | Executed by the `ToolNode` when requested. |
| **Chain** | Can be the entire logic of a single Node. |

## Quick Summary

**1-Line Recall:** **LangChain provides the "verbs" (prompt, call, parse) that LangGraph organizes into specific "sentences" (workflows).**
