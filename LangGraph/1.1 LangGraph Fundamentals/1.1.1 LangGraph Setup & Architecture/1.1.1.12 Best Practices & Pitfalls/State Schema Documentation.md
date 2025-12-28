# State Schema Documentation

## 1. Core Definition
**State Schema Documentation** is the practice of explicitly measuring and commenting the `TypedDict` or `Pydantic` model that defines the graph's state. Since the State is the API contract between nodes, it must be well-understood by all developers on the team.

## 2. Key Technical Details
*   **Docstrings**: Add python docstrings to the State class explaining what each field holds, its units, and its lifecycle (when it is populated/cleared).
*   **Annotated Types**: Use `Annotated[list, add_messages]` to explicitly show the reducer logic in the type definition itself.
*   **Field Constraints**: If using Pydantic, use `Field(..., description="...")` to make the constraints machine-readable (and human-readable).
*   **Evolution**: When adding fields, verify no name collisions with existing fields.

## 3. Mental Model
*   **Visual**: The Dictionary Legend. A map is useless without a legend explaining what the symbols mean. The State is the map; the Schema Doc is the legend.
*   **Analogy**: Database Schema. You wouldn't create a table with columns `col1`, `col2`, `col3` and no comments. You name them `user_id`, `created_at`, `email` and assert types.

## 4. Code Example
```python
class ResearchState(TypedDict):
    """
    Represents the state of the research assistant.
    """
    topic: str # The user's original query
    
    # List of documents found so far; strictly append-only
    documents: Annotated[list[Document], operator.add] 
    
    steps_taken: int # Counter to prevent infinite loops
```

## 5. One-Line Recall
Document the state schema as if it were a public API, because for your graph's nodes, it *is* the API.
