# Retrievers & RAG Integration

**Core Definition:** **Retrievers** are the standard interface for fetching documents based on an unstructured query. They are the backbone of **Retrieval Augmented Generation (RAG)**.

**Role in LangGraph:** In a graph, "Retrieval" is often a distinct node (or tool) that populates the context in the `GraphState` before the "Model" node runs.

## Key Concepts

### 1. Vector Stores (`vectorstore`)
The database.
-   **Role:** Stores semantic embeddings of text.
-   **Common Stores:** Chroma, FAISS, Pinecone, Postgres (pgvector).
-   **Interface:** `add_documents()`, `similarity_search()`.

### 2. The Retriever Interface
The unified searcher.
-   **`vectorstore.as_retriever()`**: Turns a database into a specific search configuration (e.g., "return top 5 docs").
-   **Methods:** `get_relevant_documents(query)` is the standard entry point.
-   **Abstraction:** The LLM doesn't care if it's searching a vector DB, a keyword index, or the web—it just calls the retriever.

### 3. Advanced Retrieval Strategies
-   **MultiQueryRetriever**: Generates multiple versions of a query to catch more results.
-   **ContextualCompressionRetriever**: Reranks and shortens results to fit the context window.
-   **SelfQueryRetriever**: Uses an LLM to filter the database (e.g., "docs from 2023 only").

## LangGraph Implementation Pattern

In a typical RAG agent:

1.  **State Schema:** Contains a `query` (str) and `context` (List[Document]).
2.  **Retrieval Node:**
    ```python
    def retrieve_node(state):
        docs = retriever.invoke(state["query"])
        return {"context": docs}
    ```
3.  **Generation Node:** Reads `state["context"]` and answers.

## Corrective RAG (CRAG)

LangGraph shines in **Corrective RAG**:
-   **Retrieve Step:** Get docs.
-   **Grade Step:** Model checks if docs are relevant.
-   **Branch:**
    -   *If good:* Generate answer.
    -   *If bad:* Branch to a "Web Search" node to supplement the bad context.

## Quick Summary

**1-Line Recall:** **Retrievers fetch data; LangGraph orchestrates the loop of "Retrieve -> Grade -> Generate" that makes RAG reliable.**
