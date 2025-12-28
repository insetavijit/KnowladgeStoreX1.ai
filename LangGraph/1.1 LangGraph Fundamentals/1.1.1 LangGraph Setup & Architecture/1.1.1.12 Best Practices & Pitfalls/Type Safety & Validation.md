# Type Safety & Validation

## 1. Core Definition
**Type Safety & Validation** involves rigorously defining the schema of your graph's state (using `TypedDict` or `Pydantic`) and enforcing it at runtime. This prevents common "agentic" bugs where an LLM hallucinates a malformed response (e.g., missing keys) that crashes the next node.

## 2. Key Technical Details
*   **Pydantic Models**: Preferred over simple dicts for complex state, as they provide runtime validation (e.g., ensuring a "score" is actually a float between 0-1).
*   **Output Parsers**: Use LangChain's structured output parsers (or OpenAI function calling) to coerce LLM output into your strict schema *before* it updates the state.
*   **Graph Validation**: LangGraph checks that nodes return updates consistent with the state schema (to some extent).
*   **Fail Fast**: It is better to fail at the validation boundary (and potentially retry) than to let corrupt data pollute the state and crash the graph 10 steps later.

## 3. Mental Model
*   **Visual**: A shape-sorter toy. The square block (Data) must fit through the square hole (Type Definition). If it's a triangle, it gets rejected immediately, rather than jamming the internal gears.
*   **Analogy**: Passport Control. You verify the document is valid *before* letting the person into the country, not while they are checking into a hotel 3 days later.

## 4. Code Example (Pydantic State)
```python
from pydantic import BaseModel, Field

class AgentState(BaseModel):
    query: str
    steps: list[str] = Field(default_factory=list)
    final_answer: str | None = None

# Using Pydantic allows easier validation in nodes
def node(state: AgentState):
    # IDE gives autocompletion on state.query
    return {"steps": ["step1"]} # LangGraph merges this back
```

## 5. One-Line Recall
Strict typing and runtime validation prevent "garbage in, garbage out" scenarios typical in probabilistic LLM applications.
