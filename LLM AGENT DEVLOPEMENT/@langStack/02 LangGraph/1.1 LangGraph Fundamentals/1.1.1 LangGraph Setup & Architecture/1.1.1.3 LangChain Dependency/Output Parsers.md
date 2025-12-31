# Output Parsers

**Core Definition:** **Output Parsers** are responsible for transforming the raw output of an LLM (typically a string or a message object) into a more useful, structured format (JSON, Pydantic object, List, etc.).

**Role in LangGraph:** While nodes *can* just return raw messages, parsers are useful for "Router Nodes" that need to make programmatic decisions based on the model's output (e.g., "if intent == 'search', go to search_node").

## Common Parsers

### 1. `StrOutputParser`
The simplest parser.
-   **Input:** `AIMessage(content="Hello")`
-   **Output:** `"Hello"` (string)
-   **Usage:** Used when you just want the text body and don't care about metadata.

### 2. `JsonOutputParser`
Extracts a JSON object from the text.
-   **Usage:** When you ask the model to "Return JSON," this parser reliably finds the JSON blob (even if surrounded by extra text) and converts it to a Python dict.

### 3. `PydanticOutputParser`
The content-safety parser.
-   **Input:** Text.
-   **Output:** An instance of a specific Pydantic class.
-   **Mechanism:** It generates "format instructions" to tell the model the exact schema to follow, then validates the result.

## The Shift to `with_structured_output`

Modern LangChain/LangGraph often bypasses standalone parsers in favor of **Model-Native Structured Output**.

-   **Old Way:** Prompt engineering + Output Parser.
-   **New Way:** `llm.with_structured_output(MyClass)`
    -   This uses the model's native "Function Calling" or "JSON Mode" API to guarantee structure at the generation level.

## Handling Errors

Parsers can fail if the model output is malformed.
-   **`OutputFixingParser`**: If parsing fails, this parser sends the bad output + the error back to the LLM and asks it to fix it.
-   **LangGraph Pattern:** In a graph, you might catch a parsing error and route to a "correction node" explicitly, rather than auto-fixing invisibly.

## Quick Summary

**1-Line Recall:** **Output Parsers turn LLM text into code-usable data; however, native `with_structured_output` is widely replacing them for structured tasks.**
