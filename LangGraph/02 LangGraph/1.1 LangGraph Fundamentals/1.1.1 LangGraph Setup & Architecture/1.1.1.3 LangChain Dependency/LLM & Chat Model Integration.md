# LLM & Chat Model Integration

**Core Definition:** **Model Integration** refers to how LangChain wraps proprietary APIs (OpenAI, Anthropic, Google) into standard `BaseChatModel` classes, normalizing inputs, outputs, error handling, and tool binding.

**Role in LangGraph:** Agents are driven by models. LangGraph nodes delegate the "thinking" to these integrated models.

## Key Concepts

### 1. Integration Packages
LangChain has split into partner packages to reduce bloat.
-   `langchain-openai`: `ChatOpenAI`, `OpenAIEmbeddings`.
-   `langchain-anthropic`: `ChatAnthropic`.
-   `langchain-google-vertexai`: `ChatVertexAI`.
-   **Community:** `langchain-community` holds community-maintained integrations (Ollama, HuggingFace).

### 2. Standardization Features
Regardless of the provider, you get:
-   **`bind_tools()`**: A unified way to attach tools. LangChain handles converting your Python functions to OpenAI JSON schemas, Anthropic XML/JSON tools, etc.
-   **`with_structured_output()`**: A unified way to force the model to return structured data (Pydantic objects).
-   **`stream()`**: Unified token-by-token streaming, even if the backend APIs differ.

### 3. Key Parameters
-   **`temperature`**: Creativity (0.0 = deterministic, 1.0 = creative).
-   **`model_name`**: The specific backend version (e.g., `gpt-4o`, `claude-3-opus`).
-   **`max_tokens`**: Hard limit on output length.
-   **`stop`**: Sequences that force the model to halt generation.

### 4. Local Models (Ollama/LlamaCpp)
LangChain treats local models just like API models.
-   **`ChatOllama`**: Runs models like Llama 3 locally.
-   **Benefit:** You can prototype an agent with GPT-4 and switch to Llama 3 just by changing the class instantiation.

## LangGraph Implementation

In LangGraph, the integration is usually instantiated once and passed around or imported.

```python
from langchain_openai import ChatOpenAI
from langchain_anthropic import ChatAnthropic

# Easy switching
llm_gpt = ChatOpenAI(model="gpt-4o")
llm_claude = ChatAnthropic(model="claude-3-5-sonnet-20240620")

# The node logic remains the same
def call_model(state):
    return {"messages": [llm_gpt.invoke(state["messages"])]}
```

## Quick Summary

**1-Line Recall:** **LangChain standardizes model APIs (invoke, bind_tools) so your graph logic doesn't care if it's talking to GPT-4 or Claude.**
