# Minimal State Size

## 1. Core Definition
**Minimal State Size** refers to the practice of keeping the `State` object as lean as possible. In LangGraph, the state is serialized and stored (checkpointed) at every step. Large state objects bloat storage, increase network latency (if fetching from remote DBs), and slow down LLM context filling if blindly passed to the model.

## 2. Key Technical Details
*   **Checkpoint Overhead**: Every node transition writes to the DB. A 10MB state = 10MB write *per step*. For a 50-step agent, that's 500MB of I/O.
*   **Pruning**: Remove intermediate artifacts once they are no longer needed. For example, if you extracted text from a PDF, store the text, not the binary PDF content in the state.
*   **Reference vs Value**: For large objects (images, huge datasets), store a *reference* (S3 URL, File Path, ID) in the main graph state, and fetch the actual data only within the node that needs it.
*   **Context Window**: Feeding a massive state directly to an LLM `state["messages"]` without filtering wastes tokens and money.

## 3. Mental Model
*   **Visual**: A backpacker. You only carry what you need for the hike (maps, water, food). You don't carry your entire wardrobe and furniture; you leave that at home (Database/Blob Store) and just bring the keys (References).
*   **Analogy**: RAM vs Disk. The Graph State is like RAM—fast, expensive, limited. Your Database is Disk—slow, cheap, huge. Don't load the whole Disk into RAM.

## 4. Code Example (Optimizing State)
```python
# Bad: Storing huge data directly
class State(TypedDict):
    raw_html: str # 5MB string
    summary: str

# Good: Storing reference
class State(TypedDict):
    doc_id: str   # UUID pointing to DB/S3
    summary: str

def processing_node(state):
    # Fetch huge data only when needed inside the node
    raw_html = db.get(state["doc_id"])
    return {"summary": summarize(raw_html)}
```

## 5. One-Line Recall
Keep state small for performance; store large data externally and pass references.
