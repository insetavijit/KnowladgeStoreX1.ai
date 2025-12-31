# Document Loaders & Embeddings

**Core Definition:** These are the **Data Ingestion** components. Loaders bring data *in* from the world; Embeddings convert that data into *numbers* (vectors) so the computer can understand its meaning.

**Role in LangGraph:** Essential for any agent that needs to read files, scrape the web, or access a knowledge base (RAG).

## Document Loaders

The first step of RAG: Getting the text.
-   **Wrapper Pattern:** LangChain wraps hundreds of data sources (PDF, CSV, Notion, Slack, YouTube) into a standard `.load()` interface.
-   **`WebBaseLoader`**: The go-to for scraping websites.
-   **`PyPDFLoader`**: Parses PDFs.

**Lazy Loading:**
-   For massive datasets, you use `.lazy_load()`, which yields documents one by one (generator) instead of loading 10GB into RAM at once.

## Text Splitters

You can't embed a whole book at once. You must split it.
-   **`RecursiveCharacterTextSplitter`**: The standard choice. It tries to split by paragraphs, then sentences, then words, keeping context together.

## Embeddings

The "translator" that turns text into math.
-   **Interface:** `embed_documents(list_of_texts)` -> `list_of_vectors`.
-   **`OpenAIEmbeddings`**: Industry standard (text-embedding-3-small).
-   **`HuggingFaceEmbeddings`**: Runs locally (free).

**Why it matters:**
The vector store searches for "concepts," not just keywords.
*   Query: "dog"
*   Result: "puppy" (Similiar vector, even if the word "dog" isn't there).

## LangGraph Usage

Agents often have a specialized **"Ingestion Node"** or workflow.
1.  **Loader Node:** Scrape a URL provided by the user.
2.  **Split Node:** Chunk the text.
3.  **Embed Node:** Vectorize and store in a temp vector store.
4.  **Retrieve:** Agent queries this new knowledge.

## Quick Summary

**1-Line Recall:** **Loaders read data; Splitters chop it up; Embeddings turn it into vectors for semantic search.**
