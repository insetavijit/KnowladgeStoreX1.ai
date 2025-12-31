# Prompts & Templates

**Core Definition:** **Prompts** are the instructions sent to the LLM. LangChain's template system allows these instructions to be dynamic, modular, and reusable.

**Role in LangGraph:** Agents rely on a "System Prompt" to define their persona and capabilities. LangChain templates inject the dynamic `GraphState` (like conversation history) into this prompt.

## Key Template Types

### 1. `ChatPromptTemplate`
The standard for chat models. It structures the conversation into roles.
-   **System**: "You are a helpful assistant..."
-   **Placeholder**: Inserts the moving window of chat history.
-   **Human**: The user's latest input.

```python
prompt = ChatPromptTemplate.from_messages([
    ("system", "You are a helpful assistant."),
    MessagesPlaceholder(variable_name="messages"),
])
```

### 2. `MessagesPlaceholder`
Critical for LangGraph. It tells the template: *"Insert the list of messages from the state dictionary right here."*
-   Without this, you'd have to manually format the list of messages into a string.

### 3. `FewShotChatMessagePromptTemplate`
Used to provide "in-context learning" examples to the model.
-   Improves reliability for complex tasks by showing "Input -> Output" examples before the actual task.

## Advanced Patterns

### 1. Partial Formatting
Binding values to a prompt *before* the chain runs.
-   Example: Binding the current date or a user ID so the graph doesn't need to carry it in the main state.

### 2. Validating Templates
LangChain validates that all variables in the f-string (`{variable}`) match the inputs provided. This catches missing data errors early.

### 3. Hub Integration (`langchain-hub`)
You can pull prompts from the community hub instead of hardcoding them.
`prompt = hub.pull("hwchase17/openai-functions-agent")`
-   This keeps your Python code clean and lets non-engineers edit prompts in the UI.

## LangGraph Implementation

A typical node transforms the state into a prompt:

```python
# State has {"messages": [...]}
# Prompt has MessagesPlaceholder("messages")

chain = prompt | llm
response = chain.invoke(state) # Auto-magic mapping of state dict to prompt inputs
```

## Quick Summary

**1-Line Recall:** **ChatPromptTemplate structures the agent's interaction, using MessagesPlaceholder to dynamically inject the graph's message history.**
