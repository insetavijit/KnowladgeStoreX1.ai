# Input & Output Handling

**Core Definition:** How data enters and leaves the graph execution boundary.

## Input: Partial Dicts
You typically only provide the *start* configuration.
```python
# State has {messages, user_id, memory, ...}
# Input only needs:
input = {"messages": [("user", "Hello")]}
```
Validation: LangGraph checks if `messages` exists in the schema.

## Output: Final State
By default, `invoke` returns the state at `END`.

## Controlling Output (Selection)
If your state is huge (contains embedding vectors), you might not want it all returned over the wire.
*Currently, you mostly get the whole dict. In LangServe, you can define output schemas to filter this.*

## Type Conversions
LangGraph tries to coerce inputs.
-   If schema expects `List[BaseMessage]` and you pass `[{"role": "user", "content": "hi"}]`, it often auto-converts (if using `add_messages`).
-   However, explicit instantiation `[HumanMessage(...)]` is safer.

## Quick Summary

**1-Line Recall:** **Inputs are partial state updates; Outputs are the final full state; standard LangChain type coercion often applies to inputs.**
