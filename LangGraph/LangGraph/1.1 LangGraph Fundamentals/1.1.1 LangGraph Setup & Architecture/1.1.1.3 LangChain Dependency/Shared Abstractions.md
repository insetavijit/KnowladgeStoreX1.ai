# Shared Abstractions

**Core Definition:** **Shared Abstractions** are the common interfaces and base classes that allow LangChain (and by extension, LangGraph) to be modular and agnostic to specific providers or implementations.

**Why it matters:** Because all components share a common interface (the `Runnable` protocol), you can swap an OpenAI model for an Anthropic one, or a custom tool for a built-in one, without rewriting your graph logic.

## Key Abstractions

### 1. The Runnable Protocol (`Runnable`)
The most important abstraction in modern LangChain.
-   **Definition:** A standard interface for any component that can be invoked, batched, or streamed.
-   **Methods:** `invoke`, `ainvoke`, `stream`, `astream`, `batch`, `abatch`.
-   **Polymorphism:** A Prompt, a Model, a Parser, and a Chain are ALL Runnables.
-   **LangGraph Connection:** Every Node in a LangGraph is essentially a Runnable (or calls one).

### 2. Base Language Model (`BaseLanguageModel`)
The parent class for all LLMs.
-   **`BaseLLM`**: Interface for string-in/string-out models.
-   **`BaseChatModel`**: Interface for message-list-in/message-out models.
-   **Impact:** You can type-hint your functions with `BaseChatModel` and accept *any* chat model (OpenAI, Vertex, Bedrock).

### 3. Base Tool (`BaseTool`)
The parent class for all tools.
-   **Key Attributes:** `name` (unique ID), `description` (for the LLM), `args_schema` (Pydantic model of inputs).
-   **Standardization:** Ensures that the model knows *how* to call the tool regardless of what the tool actually does.

### 4. Base Message (`BaseMessage`)
The atoms of conversation.
-   **Types:** `SystemMessage`, `HumanMessage`, `AIMessage`, `ToolMessage`.
-   **Content:** Text (string) or a list of content blocks (for multimodal).
-   **LangGraph Connection:** The `GraphState` is almost always a list of `BaseMessage` objects.

### 5. Document (`Document`)
The standard unit of text data.
-   **Structure:** Has `page_content` (str) and `metadata` (dict).
-   **Usage:** Retrievers return lists of specific `Document` objects, standardizing how data is passed from a database to the context window.

## LangGraph Usage Example

Because of shared abstractions, you can define a node that works with *any* compliant component:

```python
# Accepts ANY Chat Model due to the BaseChatModel abstraction
def model_node(state: AgentState, model: BaseChatModel):
    response = model.invoke(state["messages"])
    return {"messages": [response]}
```

## Quick Summary

**1-Line Recall:** **Shared abstractions (Runnable, BaseChatModel, BaseTool) allow LangGraph to be modular and "pluggable" with any provider.**
