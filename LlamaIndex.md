### **1.1 LlamaIndex Fundamentals**

Master LlamaIndex (formerly GPT Index) as the essential framework for building LLM-powered applications with your own data. Learn core concepts, document loading, indexing, and querying. Think in RAG (Retrieval-Augmented Generation)—not just raw LLM APIs, but intelligent systems that combine retrieval with generation. Understand how LlamaIndex bridges your data and LLMs, enabling production-ready AI applications. This prevents naive implementations and establishes patterns for scalable LLM apps. Jobs expect RAG knowledge; basic prompt engineering is insufficient.

|Topic|Focus & Purpose|
|---|---|
|**[[1.1.1 LlamaIndex Setup & Architecture]]**|Installation (pip install llama-index); API key configuration (OpenAI, etc.); project structure; core components (documents, nodes, indexes, query engines); LlamaIndex vs LangChain; when to use LlamaIndex. Foundation setup.|
|**[[1.1.2 Documents & Data Loading]]**|Document objects; SimpleDirectoryReader; loading PDFs, text files, markdown; web scraping loaders; database loaders; custom loaders; document metadata; chunking strategies. Data ingestion.|
|**[[1.1.3 Nodes & Text Splitting]]**|Node objects; NodeParser; chunk size and overlap; sentence splitters; semantic splitters; hierarchical nodes; node relationships; metadata extraction. Document processing.|
|**[[1.1.4 Indexes & Storage]]**|VectorStoreIndex; ListIndex; TreeIndex; KeywordTableIndex; index types comparison; when to use each; storage context; persisting indexes; loading saved indexes. Core indexing.|
|**[[1.1.5 Query Engines Basics]]**|Creating query engines; query() method; response objects; response modes (compact, tree_summarize, refine); streaming responses; query configuration. Querying foundation.|
|**[[1.1.6 Embeddings & Vector Stores]]**|Embedding models (OpenAI, HuggingFace); text-embedding-ada-002; local embeddings; embedding dimensions; vector stores (Pinecone, Chroma, Weaviate); similarity search. Semantic understanding.|
|**[[1.1.7 LLM Integration]]**|LLM configuration; OpenAI models (GPT-4, GPT-3.5); custom LLMs; temperature settings; max tokens; model selection; API costs; local LLMs (Ollama, LlamaCPP). Model integration.|
|**[[1.1.8 Response Synthesis]]**|Response modes; refine mode; compact mode; tree summarize; simple summarize; no text; streaming; when to use each mode. Answer generation.|

### **1.2 Advanced Retrieval Techniques**

Master sophisticated retrieval strategies essential for production RAG systems. Learn hybrid search, reranking, query transformations, and multi-modal retrieval. Understand how to improve relevance, handle complex queries, and optimize retrieval performance. RAG quality depends on retrieval—poor retrieval means poor responses regardless of LLM quality. This section covers techniques that separate basic demos from production systems.

|Topic|Focus & Purpose|
|---|---|
|**[[1.2.1 Vector Search & Similarity]]**|Cosine similarity; euclidean distance; top_k retrieval; similarity thresholds; vector search optimization; embedding quality impact; retrieval evaluation. Core retrieval mechanism.|
|**[[1.2.2 Hybrid Search]]**|Combining vector and keyword search; BM25 algorithm; fusion strategies; reciprocal rank fusion; weighted combinations; when hybrid search helps. Enhanced retrieval.|
|**[[1.2.3 Reranking Strategies]]**|Reranker models; Cohere rerank; cross-encoder reranking; LLM-based reranking; relevance scoring; two-stage retrieval; reranking performance. Improving results.|
|**[[1.2.4 Query Transformations]]**|Query rewriting; HyDE (Hypothetical Document Embeddings); query expansion; multi-query retrieval; step-back prompting; query decomposition. Smarter queries.|
|**[[1.2.5 Metadata Filtering]]**|Metadata extraction; filtering by metadata; date filters; category filters; hybrid filtering; metadata-based routing; structured metadata. Precise retrieval.|
|**[[1.2.6 Sentence Window Retrieval]]**|Window retrieval concept; context windows; sentence boundaries; expanding retrieved chunks; balancing specificity and context. Context preservation.|
|**[[1.2.7 Auto-merging Retrieval]]**|Hierarchical node structures; parent-child relationships; auto-merging strategy; recursive retrieval; when auto-merging helps; performance considerations. Intelligent chunk merging.|
|**[[1.2.8 Retrieval Evaluation]]**|Hit rate; MRR (Mean Reciprocal Rank); NDCG; faithfulness; relevancy; evaluation datasets; A/B testing retrieval; measuring quality. Quantifying performance.|

### **1.3 Query Engines & Agents**

Master advanced query patterns and agentic workflows. Learn routers, sub-question engines, multi-document queries, and ReAct agents. Understand when to use query engines vs agents, how to compose multiple data sources, and build autonomous systems. Agents enable dynamic tool use and multi-step reasoning—essential for complex applications. This section covers orchestration patterns for production LLM applications.

|Topic|Focus & Purpose|
|---|---|
|**[[1.3.1 Query Engine Patterns]]**|RouterQueryEngine; SubQuestionQueryEngine; RetrieverQueryEngine; custom query engines; query pipelines; conditional routing; engine composition. Advanced querying.|
|**[[1.3.2 Routers & Selectors]]**|LLMSingleSelector; LLMMultiSelector; PydanticMultiSelector; routing logic; selector prompts; dynamic routing; multi-index routing. Intelligent routing.|
|**[[1.3.3 Sub-Question Decomposition]]**|Breaking complex queries; sub-question generation; parallel sub-queries; answer synthesis from sub-answers; handling dependencies; multi-hop reasoning. Complex query handling.|
|**[[1.3.4 Multi-Document Queries]]**|Querying across indexes; document summarization; comparative queries; cross-document synthesis; document routing; handling large document sets. Multiple source integration.|
|**[[1.3.5 ReAct Agents]]**|ReAct framework; observation-thought-action loop; tool use; agent reasoning; function calling; agent memory; when to use agents vs query engines. Autonomous systems.|
|**[[1.3.6 Tools & Function Calling]]**|QueryEngineTool; FunctionTool; custom tools; tool descriptions; tool selection; parallel tool use; error handling in tools. Extending capabilities.|
|**[[1.3.7 Agent Workflows]]**|Multi-step workflows; conditional logic; loops; error recovery; workflow state; human-in-the-loop; complex orchestration. Production workflows.|
|**[[1.3.8 Memory & Context Management]]**|Conversation memory; chat history; context window management; memory summarization; long-term memory; working memory; memory persistence. Stateful interactions.|

### **1.4 Production RAG Systems**

Build production-ready RAG applications with proper architecture, monitoring, and optimization. Learn prompt engineering, evaluation frameworks, cost optimization, and system reliability. Understand streaming responses, error handling, fallbacks, and production deployment. Master observability, logging, and debugging production issues. This section covers engineering best practices that separate prototypes from production systems.

|Topic|Focus & Purpose|
|---|---|
|**[[1.4.1 Prompt Engineering for RAG]]**|System prompts; few-shot examples; prompt templates; chain-of-thought; prompt optimization; context instructions; handling hallucinations. Effective prompting.|
|**[[1.4.2 Streaming & Real-time Responses]]**|Streaming query engines; streaming agents; token-by-token responses; async streaming; WebSocket integration; UI considerations. Better UX.|
|**[[1.4.3 Caching Strategies]]**|Embedding caching; response caching; cache invalidation; Redis integration; cache-aside pattern; TTL strategies; cache hit rates. Performance optimization.|
|**[[1.4.4 Cost Optimization]]**|Token usage tracking; model selection; caching for cost reduction; batch processing; prompt optimization; embedding reuse; monitoring costs. Controlling expenses.|
|**[[1.4.5 Error Handling & Fallbacks]]**|Retry logic; exponential backoff; fallback responses; error types; graceful degradation; timeout handling; error logging. System reliability.|
|**[[1.4.6 Observability & Logging]]**|LlamaIndex callbacks; tracing; monitoring retrieval; logging queries; performance metrics; debugging tools; observability platforms (LangSmith, Phoenix). Production monitoring.|
|**[[1.4.7 Evaluation Frameworks]]**|Faithfulness evaluation; relevancy evaluation; correctness evaluation; context relevancy; answer relevancy; automated evaluation; human evaluation. Quality assurance.|
|**[[1.4.8 Security & Privacy]]**|API key management; input sanitization; output filtering; PII detection; data privacy; secure storage; access control. Secure systems.|

### **1.5 Vector Databases & Storage**

Master vector database integration essential for production RAG. Learn Pinecone, Chroma, Weaviate, Qdrant, and choosing the right vector store. Understand indexes, metadata filtering, hybrid search, and performance optimization. Learn data ingestion pipelines, incremental updates, and backup strategies. Vector stores are the foundation of RAG—proper setup and management are critical for performance and cost.

|Topic|Focus & Purpose|
|---|---|
|**[[1.5.1 Vector Store Concepts]]**|Vector database fundamentals; HNSW algorithm; IVF indexes; approximate nearest neighbor (ANN); exact vs approximate search; index types; performance trade-offs. Understanding vector DBs.|
|**[[1.5.2 Pinecone Integration]]**|Pinecone setup; creating indexes; namespaces; metadata filtering; hybrid search; upsert operations; querying Pinecone; pricing model. Managed vector DB.|
|**[[1.5.3 Chroma Integration]]**|Chroma local setup; persistent storage; collections; metadata filtering; embeddings management; client/server mode; when Chroma fits. Open-source option.|
|**[[1.5.4 Weaviate Integration]]**|Weaviate setup; schema definition; classes and properties; hybrid search; generative search; filtering; backups; cloud vs self-hosted. Advanced features.|
|**[[1.5.5 Qdrant Integration]]**|Qdrant setup; collections; points and payloads; filtering; batch operations; snapshots; quantization; performance tuning. High-performance option.|
|**[[1.5.6 Local Vector Stores]]**|SimpleVectorStore; FAISS integration; local storage; when local stores work; limitations; transitioning to cloud; development workflows. Development-friendly.|
|**[[1.5.7 Data Ingestion Pipelines]]**|Batch ingestion; incremental updates; deduplication; change detection; scheduling ingestion; error handling; monitoring pipelines. Data management.|
|**[[1.5.8 Vector Store Selection]]**|Comparing vector databases; cost considerations; scaling; performance; features; managed vs self-hosted; migration strategies. Choosing the right DB.|

### **1.6 Multi-Modal & Specialized RAG**

Extend RAG beyond text to images, tables, code, and structured data. Learn multi-modal embeddings, vision-language models, table understanding, and code search. Master SQL generation, knowledge graphs, and specialized document types. Understand domain-specific RAG for legal, medical, financial documents. This section covers advanced RAG applications beyond simple text retrieval.

|Topic|Focus & Purpose|
|---|---|
|**[[1.6.1 Multi-Modal RAG]]**|CLIP embeddings; vision-language models; image retrieval; GPT-4 Vision integration; multi-modal indexing; image-text search; OCR integration. Beyond text.|
|**[[1.6.2 Table Understanding]]**|Parsing tables; structured data extraction; table QA; pandas integration; table-text hybrid retrieval; complex table queries. Tabular data.|
|**[[1.6.3 Code Search & Understanding]]**|Code indexing; AST parsing; code embeddings; function-level retrieval; code documentation; repository search; semantic code search. Developer tools.|
|**[[1.6.4 SQL Generation]]**|Text-to-SQL; SQLDatabase integration; NLSQLTableQueryEngine; schema understanding; query validation; SQL safety; database connections. Natural language queries.|
|**[[1.6.5 Knowledge Graphs]]**|KnowledgeGraphIndex; entity extraction; relationship modeling; graph traversal; Neo4j integration; graph RAG; when graphs help. Structured knowledge.|
|**[[1.6.6 PDF & Document Processing]]**|PDF parsing; table extraction; figure extraction; document layout; OCR; multi-column handling; complex document structures. Document understanding.|
|**[[1.6.7 Domain-Specific RAG]]**|Legal documents; medical records; financial reports; scientific papers; specialized preprocessing; domain embeddings; compliance. Vertical solutions.|
|**[[1.6.8 Structured Output]]**|Pydantic output parsing; structured data extraction; JSON mode; function calling for structure; schema-driven retrieval. Formatted responses.|

### **1.7 Fine-Tuning & Customization**

Optimize RAG systems through fine-tuning embeddings, training rerankers, and customizing components. Learn embedding fine-tuning, distillation, and domain adaptation. Master custom node parsers, query transformations, and response synthesizers. Understand when fine-tuning helps vs when it's unnecessary. This section covers advanced optimization for specialized use cases and maximum performance.

|Topic|Focus & Purpose|
|---|---|
|**[[1.7.1 Embedding Fine-Tuning]]**|When to fine-tune embeddings; training data preparation; contrastive learning; fine-tuning process; evaluation; domain-specific embeddings; fine-tuning costs. Custom embeddings.|
|**[[1.7.2 Custom Node Parsers]]**|Implementing custom parsers; specialized splitting logic; metadata extraction; document-specific parsing; hierarchical parsing; parser composition. Tailored processing.|
|**[[1.7.3 Custom Retrievers]]**|BaseRetriever implementation; custom retrieval logic; combining retrievers; specialized retrieval strategies; performance optimization. Retrieval flexibility.|
|**[[1.7.4 Custom Response Synthesizers]]**|BaseSynthesizer implementation; custom synthesis logic; specialized output formats; multi-source synthesis; synthesis optimization. Response control.|
|**[[1.7.5 Prompt Customization]]**|Custom prompt templates; system messages; few-shot examples; prompt versioning; A/B testing prompts; prompt libraries. Prompt management.|
|**[[1.7.6 Reranker Training]]**|Training cross-encoders; ranking datasets; fine-tuning rerankers; evaluation metrics; deployment considerations. Better ranking.|
|**[[1.7.7 Query Understanding]]**|Intent detection; entity extraction; query classification; query expansion; query validation; understanding user needs. Smarter interpretation.|
|**[[1.7.8 Domain Adaptation]]**|Adapting to specific domains; specialized vocabularies; domain knowledge injection; industry-specific patterns; vertical optimization. Specialized systems.|

### **1.8 Scalability & Performance**

Build RAG systems that scale to millions of documents and thousands of users. Master batch processing, distributed indexing, load balancing, and caching. Learn async patterns, parallel processing, and resource optimization. Understand infrastructure requirements, deployment strategies, and monitoring at scale. This section covers production engineering for enterprise RAG applications.

|Topic|Focus & Purpose|
|---|---|
|**[[1.8.1 Async Operations]]**|Async query engines; asyncio patterns; concurrent queries; async retrievers; non-blocking operations; async best practices. Performance through concurrency.|
|**[[1.8.2 Batch Processing]]**|Batch document ingestion; parallel indexing; batch embeddings; chunked processing; progress tracking; error handling in batches. Efficient bulk operations.|
|**[[1.8.3 Distributed Systems]]**|Horizontal scaling; load balancing; distributed vector stores; sharding strategies; consistency; distributed caching. Scaling out.|
|**[[1.8.4 Performance Optimization]]**|Profiling queries; bottleneck identification; index optimization; query optimization; caching strategies; resource utilization. Speed improvements.|
|**[[1.8.5 Resource Management]]**|Memory optimization; connection pooling; rate limiting; quota management; resource cleanup; garbage collection. Efficient resource use.|
|**[[1.8.6 Infrastructure & Deployment]]**|Docker containerization; Kubernetes deployment; cloud deployment (AWS, GCP, Azure); serverless RAG; infrastructure as code. Production infrastructure.|
|**[[1.8.7 Monitoring & Alerting]]**|Metrics collection; latency monitoring; error rates; cost monitoring; alerting systems; dashboards; SLOs/SLIs. Operational visibility.|
|**[[1.8.8 Scaling Strategies]]**|Horizontal vs vertical scaling; auto-scaling; capacity planning; load testing; performance benchmarking; scaling bottlenecks. Growth planning.|

### **1.9 Advanced Patterns & Architectures**

Master sophisticated RAG architectures used in production systems. Learn FLARE, self-RAG, corrective RAG, and adaptive retrieval. Understand RAG fusion, iterative retrieval, and agentic RAG patterns. Learn multi-tenant systems, versioning strategies, and A/B testing frameworks. This section covers cutting-edge patterns from research and production systems—essential for senior-level RAG engineering.

|Topic|Focus & Purpose|
|---|---|
|**[[1.9.1 FLARE (Active Retrieval)]]**|Forward-looking active retrieval; uncertainty detection; dynamic retrieval; iterative refinement; when FLARE helps. Adaptive systems.|
|**[[1.9.2 Self-RAG & Reflection]]**|Self-assessment; retrieval decision-making; critique generation; self-correction; reflection patterns. Introspective systems.|
|**[[1.9.3 Corrective RAG (CRAG)]]**|Relevance verification; document grading; web search fallback; correction strategies; quality gates. Error correction.|
|**[[1.9.4 RAG Fusion]]**|Multiple query generation; parallel retrieval; reciprocal rank fusion; ensemble methods; fusion strategies. Combined approaches.|
|**[[1.9.5 Iterative Retrieval]]**|Multi-turn retrieval; retrieval refinement; context accumulation; follow-up queries; conversation-aware retrieval. Progressive refinement.|
|**[[1.9.6 Agentic RAG]]**|Tool-augmented retrieval; planning and reasoning; multi-step workflows; tool selection; agent architectures for RAG. Autonomous RAG.|
|**[[1.9.7 Multi-Tenant Systems]]**|Tenant isolation; namespace management; access control; resource quotas; tenant-specific customization; scaling multi-tenancy. Enterprise architectures.|
|**[[1.9.8 A/B Testing & Experimentation]]**|Experiment design; traffic splitting; metric collection; statistical significance; feature flags; gradual rollout. Continuous improvement.|

### **1.10 Integration & Ecosystem**

Master integrating LlamaIndex with popular frameworks and tools. Learn LangChain interop, FastAPI/Flask integration, Streamlit apps, and React frontends. Understand database integrations, authentication systems, and third-party services. Learn deployment platforms, CI/CD pipelines, and monitoring services. This section covers building complete applications that combine LlamaIndex with the broader ecosystem.

|Topic|Focus & Purpose|
|---|---|
|**[[1.10.1 Web Framework Integration]]**|FastAPI integration; Flask integration; API design; request handling; response formatting; WebSocket support; REST vs GraphQL. Backend services.|
|**[[1.10.2 Frontend Integration]]**|React integration; Vue.js integration; streaming in UI; chat interfaces; file upload handling; real-time updates. User interfaces.|
|**[[1.10.3 Streamlit Applications]]**|Streamlit basics; chat interface; file uploaders; session state; caching; deployment; Streamlit Cloud; rapid prototyping. Quick apps.|
|**[[1.10.4 LangChain Interoperability]]**|LangChain integration; converting between frameworks; using LangChain tools in LlamaIndex; when to use each; hybrid approaches. Framework compatibility.|
|**[[1.10.5 Database Integration]]**|PostgreSQL integration; MongoDB integration; document stores; metadata storage; audit logs; user management. Persistent storage.|
|**[[1.10.6 Authentication & Authorization]]**|User authentication; API key management; JWT tokens; role-based access; tenant isolation; secure endpoints. Access control.|
|**[[1.10.7 Cloud Platforms]]**|AWS deployment; Google Cloud; Azure; Vercel; Railway; Heroku; serverless options; cloud storage. Hosting solutions.|
|**[[1.10.8 MLOps & Deployment]]**|CI/CD pipelines; automated testing; model versioning; deployment automation; rollback strategies; blue-green deployment. Professional deployment.|
