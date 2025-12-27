### **1.1 Prompt Engineering Fundamentals**

Master prompt engineering as the essential skill for working with Large Language Models. Learn prompt structure, instruction design, context management, and output control. Think systematically—not trial-and-error, but principled techniques backed by research. Understand how LLMs process prompts, tokenization, and context windows. This prevents ineffective prompting and establishes patterns for reliable LLM applications. Jobs expect prompt engineering expertise; basic prompting skills are insufficient for production systems.

|Topic|Focus & Purpose|
|---|---|
|**[[1.1.1 LLM Basics & Tokenization]]**|How LLMs work; transformer architecture overview; tokens vs words; tokenization process; context windows; token limits; counting tokens; token efficiency. Foundation understanding.|
|**[[1.1.2 Prompt Anatomy]]**|System messages; user messages; assistant messages; role definitions; instruction placement; context structure; output format specification. Prompt components.|
|**[[1.1.3 Instruction Design]]**|Clear instructions; specificity; imperative vs declarative; task framing; instruction length; explicit vs implicit; ambiguity avoidance. Effective instructions.|
|**[[1.1.4 Context Management]]**|Providing context; relevant information; context placement; context length; prioritizing information; context window optimization. Context strategies.|
|**[[1.1.5 Output Formatting]]**|Specifying formats; JSON, XML, markdown; structured output; format examples; template specification; output validation. Controlled outputs.|
|**[[1.1.6 Temperature & Parameters]]**|Temperature setting; top-p (nucleus sampling); top-k; frequency penalty; presence penalty; parameter effects; when to adjust; deterministic vs creative. Model parameters.|
|**[[1.1.7 Prompt Iteration]]**|Testing prompts; A/B testing; prompt versions; iterative refinement; measuring quality; prompt debugging; systematic improvement. Optimization process.|
|**[[1.1.8 Common Pitfalls]]**|Vague instructions; information overload; conflicting instructions; assumed knowledge; format inconsistency; prompt injection vulnerabilities. Avoiding mistakes.|

### **1.2 Advanced Prompting Techniques**

Master research-backed prompting strategies that dramatically improve LLM performance. Learn few-shot learning, chain-of-thought, self-consistency, and tree-of-thoughts. Understand when to use each technique, how they work, and their trade-offs. These techniques are proven in academic research and production systems—essential for complex reasoning tasks. This section covers methods that separate novice from expert prompt engineers.

|Topic|Focus & Purpose|
|---|---|
|**[[1.2.1 Zero-Shot Prompting]]**|Direct instructions; no examples; zero-shot capabilities; clear task description; when zero-shot works; zero-shot limitations; optimizing zero-shot. Baseline approach.|
|**[[1.2.2 Few-Shot Learning]]**|Example-based learning; shot selection; example diversity; example ordering; k-shot prompting; example quality; few-shot vs fine-tuning. Learning from examples.|
|**[[1.2.3 Chain-of-Thought (CoT)]]**|Step-by-step reasoning; "Let's think step by step"; explicit reasoning traces; CoT for math/logic; zero-shot CoT; few-shot CoT; when CoT helps. Research-backed reasoning.|
|**[[1.2.4 Self-Consistency]]**|Multiple reasoning paths; sampling diverse solutions; majority voting; consistency checking; temperature tuning; aggregation strategies. Ensemble reasoning.|
|**[[1.2.5 Tree-of-Thoughts (ToT)]]**|Exploring multiple paths; branching reasoning; backtracking; state evaluation; search strategies; when ToT is needed; computational cost. Advanced reasoning.|
|**[[1.2.6 ReAct (Reasoning + Acting)]]**|Interleaved reasoning and action; observation-thought-action loops; tool use with reasoning; when ReAct helps; ReAct prompting patterns. Action-oriented reasoning.|
|**[[1.2.7 Least-to-Most Prompting]]**|Problem decomposition; solving subproblems; building solutions; sequential prompting; dependency handling; complex problem solving. Incremental reasoning.|
|**[[1.2.8 Generated Knowledge]]**|Generating relevant knowledge first; knowledge-augmented prompts; two-stage prompting; when generated knowledge helps; knowledge quality. Knowledge injection.|

### **1.3 Role-Based & Persona Prompting**

Master persona design and role-based prompting for specialized tasks. Learn expert persona creation, style control, tone management, and character consistency. Understand cognitive prompting, metacognitive techniques, and perspective-taking. Role prompting dramatically improves domain-specific performance—essential for specialized applications like medical, legal, or technical assistance.

|Topic|Focus & Purpose|
|---|---|
|**[[1.3.1 Expert Personas]]**|Defining expert roles; domain expertise; specialized knowledge; professional tone; expert behavior; persona consistency. Domain specialists.|
|**[[1.3.2 Character Development]]**|Persona attributes; personality traits; knowledge boundaries; communication style; consistency maintenance; character depth. Detailed personas.|
|**[[1.3.3 Tone & Style Control]]**|Formal vs informal; technical vs casual; professional vs friendly; audience adaptation; brand voice; style guidelines. Communication style.|
|**[[1.3.4 Perspective Taking]]**|First-person vs third-person; user perspective; expert viewpoint; stakeholder perspectives; perspective shifting. Viewpoint control.|
|**[[1.3.5 Cognitive Prompting]]**|Thinking modes; analytical vs creative; critical thinking; problem-solving approaches; reasoning styles; cognitive frameworks. Mental models.|
|**[[1.3.6 Metacognitive Instructions]]**|Self-reflection prompts; uncertainty acknowledgment; confidence levels; explaining reasoning; checking work; metacognition. Self-awareness.|
|**[[1.3.7 Audience Adaptation]]**|Target audience; expertise level; age appropriateness; cultural sensitivity; accessibility; explanation depth. User-centered prompting.|
|**[[1.3.8 Consistency Maintenance]]**|Persona reinforcement; style preservation; character continuity; avoiding drift; long conversation consistency. Stable personas.|

### **1.4 Structured Output & Data Extraction**

Master techniques for extracting structured data and ensuring consistent formats. Learn JSON mode, XML generation, schema validation, and field extraction. Understand regular expressions in prompts, output parsing, and format enforcement. Structured output is critical for production systems—unreliable parsing breaks pipelines. This section covers methods for deterministic, parseable LLM outputs.

|Topic|Focus & Purpose|
|---|---|
|**[[1.4.1 JSON Output]]**|JSON mode; schema specification; nested JSON; array handling; field types; JSON validation; ensuring valid JSON. Structured data.|
|**[[1.4.2 XML & Markup]]**|XML generation; tag specification; attributes; nested structures; XHTML; markdown with structure; custom markup. Markup formats.|
|**[[1.4.3 Schema Validation]]**|Defining schemas; Pydantic models; JSON Schema; type constraints; required fields; validation rules; error handling. Type safety.|
|**[[1.4.4 Field Extraction]]**|Named entity extraction; field identification; multi-field extraction; extraction accuracy; handling missing data; confidence scores. Data parsing.|
|**[[1.4.5 Table Generation]]**|CSV format; markdown tables; HTML tables; column specification; data alignment; table validation. Tabular output.|
|**[[1.4.6 Template Filling]]**|Template specification; placeholder filling; variable substitution; template consistency; conditional templates. Formatted outputs.|
|**[[1.4.7 Classification Tasks]]**|Category assignment; multi-class classification; confidence scores; label consistency; hierarchical classification. Categorization.|
|**[[1.4.8 Regular Expressions]]**|Specifying patterns; format validation; extraction patterns; regex in prompts; pattern examples; format enforcement. Pattern matching.|

### **1.5 Context Window Optimization**

Master techniques for working within context window limits. Learn compression, summarization, prioritization, and retrieval-augmented generation. Understand token counting, context stuffing, sliding windows, and memory management. Context limits are hard constraints—exceeding them breaks applications. This section covers strategies for maximizing information within limits.

|Topic|Focus & Purpose|
|---|---|
|**[[1.5.1 Token Budget Management]]**|Counting tokens; budget allocation; token efficiency; compression techniques; essential vs optional information. Resource management.|
|**[[1.5.2 Information Prioritization]]**|Relevance ranking; importance scoring; critical information; pruning details; hierarchical information; priority-based inclusion. Smart selection.|
|**[[1.5.3 Compression Strategies]]**|Summarization; paraphrasing; abbreviation; removing redundancy; dense representation; information density. Condensing content.|
|**[[1.5.4 Sliding Window Techniques]]**|Window management; moving context; overlap strategies; conversation truncation; recency bias; sliding mechanisms. Dynamic context.|
|**[[1.5.5 Retrieval-Augmented Generation]]**|RAG fundamentals; relevant document retrieval; context injection; retrieval timing; multi-document synthesis; citation. External knowledge.|
|**[[1.5.6 Summarization in Context]]**|Progressive summarization; hierarchical summaries; rolling summaries; memory compression; conversation summaries. Context condensation.|
|**[[1.5.7 Chunking Strategies]]**|Document chunking; chunk size; overlap; semantic chunking; sentence-level; paragraph-level; optimal chunk sizes. Segmentation.|
|**[[1.5.8 Context Packing]]**|Maximizing information density; efficient formatting; removing formatting; acronyms; bullet points vs prose. Space optimization.|

### **1.6 Reasoning & Problem Solving**

Master advanced reasoning techniques for complex problem-solving. Learn decomposition, analogical reasoning, counterfactual thinking, and multi-step logic. Understand mathematical reasoning, code generation, and scientific reasoning. These techniques enable LLMs to tackle sophisticated problems—essential for technical and analytical applications.

|Topic|Focus & Purpose|
|---|---|
|**[[1.6.1 Problem Decomposition]]**|Breaking problems down; subproblem identification; dependency mapping; hierarchical breakdown; solving subproblems; synthesis. Divide and conquer.|
|**[[1.6.2 Mathematical Reasoning]]**|Step-by-step math; equation solving; verification; numerical reasoning; mathematical notation; proof techniques. Quantitative reasoning.|
|**[[1.6.3 Logical Reasoning]]**|Deductive reasoning; inductive reasoning; premise-conclusion; logical validity; syllogisms; formal logic. Structured logic.|
|**[[1.6.4 Analogical Reasoning]]**|Using analogies; comparison; transfer learning; similar problems; abstraction; pattern matching. Reasoning by analogy.|
|**[[1.6.5 Counterfactual Thinking]]**|"What if" scenarios; alternative outcomes; hypothetical reasoning; scenario analysis; exploring alternatives. Hypotheticals.|
|**[[1.6.6 Causal Reasoning]]**|Cause-effect relationships; causal chains; confounders; correlation vs causation; causal inference. Understanding causality.|
|**[[1.6.7 Multi-Hop Reasoning]]**|Connecting information; transitive reasoning; inference chains; multi-step deduction; complex connections. Connected reasoning.|
|**[[1.6.8 Verification & Validation]]**|Checking answers; self-verification; consistency checks; error detection; validation criteria; proof reading. Quality control.|

### **1.7 Safety & Alignment**

Master techniques for safe, aligned, and responsible LLM outputs. Learn content filtering, bias mitigation, toxicity prevention, and alignment techniques. Understand prompt injection defense, jailbreak prevention, and constitutional AI. Safety is non-negotiable for production systems—this section covers critical techniques for responsible AI deployment.

|Topic|Focus & Purpose|
|---|---|
|**[[1.7.1 Content Filtering]]**|Harmful content detection; output filtering; safety guidelines; content policies; moderation techniques; filter implementation. Safety measures.|
|**[[1.7.2 Bias Mitigation]]**|Identifying bias; debiasing techniques; fair representation; stereotype avoidance; inclusive language; bias testing. Fairness.|
|**[[1.7.3 Toxicity Prevention]]**|Toxic output detection; respectful language; hostile content prevention; harassment avoidance; profanity filtering. Respectful AI.|
|**[[1.7.4 Prompt Injection Defense]]**|Understanding attacks; input sanitization; instruction hierarchy; delimiter use; defense techniques; security testing. Security.|
|**[[1.7.5 Jailbreak Prevention]]**|Recognizing jailbreaks; defense strategies; alignment maintenance; refusing harmful requests; system message protection. System integrity.|
|**[[1.7.6 Constitutional AI]]**|Principle-based constraints; self-critique; value alignment; ethical guidelines; constitution specification. Principled AI.|
|**[[1.7.7 Uncertainty & Confidence]]**|Expressing uncertainty; confidence levels; acknowledging limits; avoiding overconfidence; calibration. Honest AI.|
|**[[1.7.8 Refusal Strategies]]**|When to refuse; polite refusals; explaining limitations; alternative suggestions; boundary setting. Appropriate limits.|

### **1.8 Multi-Turn & Conversational AI**

Master techniques for effective multi-turn conversations and dialogue management. Learn context maintenance, conversation flow, clarification strategies, and memory techniques. Understand turn-taking, topic tracking, and conversation repair. Multi-turn conversations require different techniques than single-turn—essential for chatbots and assistants.

|Topic|Focus & Purpose|
|---|---|
|**[[1.8.1 Conversation Context]]**|Maintaining history; referencing previous turns; context coherence; conversation memory; tracking state. Dialogue continuity.|
|**[[1.8.2 Clarification Strategies]]**|Asking questions; resolving ambiguity; confirmation requests; iterative refinement; information gathering. Understanding users.|
|**[[1.8.3 Topic Tracking]]**|Following topics; topic shifts; returning to topics; topic coherence; multi-topic handling. Conversation flow.|
|**[[1.8.4 Turn Management]]**|Turn-taking; response timing; conversation pacing; interruption handling; natural flow. Dialogue dynamics.|
|**[[1.8.5 Personalization]]**|User preferences; adaptation; learning from history; customization; personal context; relationship building. Individual users.|
|**[[1.8.6 Conversation Repair]]**|Handling misunderstandings; correction; backtracking; error recovery; apology strategies. Fixing mistakes.|
|**[[1.8.7 Proactive Engagement]]**|Asking relevant questions; making suggestions; anticipating needs; driving conversation; engagement strategies. Active participation.|
|**[[1.8.8 Conversation Closure]]**|Ending conversations; summarization; next steps; graceful exits; follow-up offers. Proper endings.|

### **1.9 Domain-Specific Prompting**

Master prompting techniques for specialized domains. Learn medical, legal, technical, creative, and educational prompting. Understand domain-specific terminology, compliance requirements, and quality standards. Each domain has unique requirements—this section covers vertical-specific techniques essential for professional applications.

|Topic|Focus & Purpose|
|---|---|
|**[[1.9.1 Technical & Code Generation]]**|Programming prompts; code quality; documentation; debugging assistance; language-specific techniques; code review. Software engineering.|
|**[[1.9.2 Medical & Healthcare]]**|Medical terminology; diagnostic assistance; treatment information; HIPAA compliance; disclaimers; evidence-based responses. Healthcare applications.|
|**[[1.9.3 Legal & Compliance]]**|Legal terminology; regulatory compliance; disclaimer requirements; jurisdictional awareness; citation requirements; risk management. Legal applications.|
|**[[1.9.4 Financial & Business]]**|Financial analysis; market research; business intelligence; risk assessment; compliance; professional standards. Business applications.|
|**[[1.9.5 Creative Writing]]**|Storytelling; character development; plot generation; style emulation; creative constraints; genre conventions. Creative applications.|
|**[[1.9.6 Educational Content]]**|Pedagogical techniques; age-appropriate content; learning objectives; scaffolding; assessment; educational standards. Teaching applications.|
|**[[1.9.7 Scientific & Research]]**|Scientific methodology; literature review; hypothesis generation; data analysis; technical accuracy; citation. Research applications.|
|**[[1.9.8 Customer Support]]**|Support workflows; troubleshooting; empathy; resolution steps; escalation; satisfaction; brand voice. Service applications.|

### **1.10 Evaluation & Testing**

Master techniques for evaluating and testing prompts systematically. Learn metrics, benchmarks, human evaluation, and automated testing. Understand A/B testing, regression testing, and continuous improvement. Proper evaluation separates guesswork from systematic optimization—essential for production-grade prompt engineering.

|Topic|Focus & Purpose|
|---|---|
|**[[1.10.1 Evaluation Metrics]]**|Accuracy; precision/recall; F1 score; BLEU/ROUGE; perplexity; human metrics; task-specific metrics. Measuring quality.|
|**[[1.10.2 Benchmark Datasets]]**|Standard benchmarks; MMLU; HellaSwag; TruthfulQA; domain-specific benchmarks; creating benchmarks. Standardized testing.|
|**[[1.10.3 Human Evaluation]]**|Annotation guidelines; inter-rater reliability; evaluation criteria; quality assessment; preference testing. Human judgment.|
|**[[1.10.4 Automated Testing]]**|Unit tests for prompts; regression testing; test suites; CI/CD integration; automated evaluation; test coverage. Systematic testing.|
|**[[1.10.5 A/B Testing]]**|Experimental design; variant testing; statistical significance; success metrics; test duration; result interpretation. Comparative testing.|
|**[[1.10.6 Error Analysis]]**|Failure modes; error patterns; systematic errors; edge cases; debugging prompts; root cause analysis. Understanding failures.|
|**[[1.10.7 Performance Monitoring]]**|Production metrics; latency; cost; quality tracking; drift detection; alerting. Ongoing monitoring.|
|**[[1.10.8 Continuous Improvement]]**|Iterative refinement; feedback loops; version control; prompt evolution; learning from production. Optimization cycle.|

### **1.11 Model-Specific Optimization**

Master techniques specific to different LLM families. Learn GPT-4 vs GPT-3.5 optimization, Claude-specific techniques, open-source model prompting, and multi-model strategies. Understand model capabilities, limitations, and cost-performance trade-offs. Each model has unique characteristics—this section covers model-specific optimization essential for production systems.

|Topic|Focus & Purpose|
|---|---|
|**[[1.11.1 GPT-4 Optimization]]**|GPT-4 capabilities; longer context; vision; function calling; multimodal prompts; cost considerations; when GPT-4 needed. Flagship model.|
|**[[1.11.2 GPT-3.5 Optimization]]**|Speed vs quality trade-offs; cost optimization; appropriate tasks; limitations; GPT-3.5-Turbo; when sufficient. Efficient model.|
|**[[1.11.3 Claude Optimization]]**|Claude-specific techniques; constitutional AI; longer context; XML preference; prompt engineering differences. Anthropic models.|
|**[[1.11.4 Open-Source Models]]**|Llama; Mistral; prompting differences; local deployment; fine-tuning; quantization; performance optimization. Open models.|
|**[[1.11.5 Model Selection]]**|Task-model matching; capability assessment; cost-performance analysis; latency requirements; model comparison. Choosing models.|
|**[[1.11.6 Multi-Model Strategies]]**|Using multiple models; routing; fallbacks; ensemble methods; cost optimization; capability complementarity. Hybrid approaches.|
|**[[1.11.7 Function Calling]]**|Tool use; function definitions; parameter specification; function calling vs prompting; error handling. Structured interaction.|
|**[[1.11.8 Vision-Language Models]]**|Image prompting; GPT-4V; Claude Vision; describing images; OCR; visual reasoning; multimodal tasks. Visual understanding.|

### **1.12 Production Prompt Engineering**

Master engineering practices for production prompt systems. Learn version control, prompt management, API integration, and deployment strategies. Understand caching, batching, rate limiting, and cost optimization. Learn observability, monitoring, and debugging production issues. This section covers enterprise-grade prompt engineering essential for scalable systems.

|Topic|Focus & Purpose|
|---|---|
|**[[1.12.1 Prompt Versioning]]**|Version control; Git for prompts; change tracking; rollback; branching; prompt repositories. Managing evolution.|
|**[[1.12.2 Prompt Management Systems]]**|Centralized storage; prompt libraries; template systems; variable injection; environment-specific prompts. Organization.|
|**[[1.12.3 API Integration]]**|SDK usage; API calls; error handling; retry logic; timeouts; authentication; rate limiting. Technical integration.|
|**[[1.12.4 Caching Strategies]]**|Response caching; cache invalidation; semantic caching; cache hit rates; cost reduction. Performance optimization.|
|**[[1.12.5 Batch Processing]]**|Batch API; async processing; job queuing; throughput optimization; cost savings; batch strategies. Bulk operations.|
|**[[1.12.6 Cost Optimization]]**|Token reduction; model selection; caching; prompt compression; batching; monitoring costs; budgeting. Controlling expenses.|
|**[[1.12.7 Observability]]**|Logging; tracing; metrics; debugging; error tracking; performance monitoring; analytics. System visibility.|
|**[[1.12.8 Deployment Strategies]]**|Blue-green deployment; canary releases; gradual rollout; feature flags; A/B testing infrastructure. Production deployment.|

### **1.13 Emerging Techniques & Research**

Master cutting-edge prompt engineering techniques from recent research. Learn prompt chaining, automatic prompt engineering, meta-prompting, and prompt tuning. Understand constitutional AI, instruction tuning, and RLHF implications. Stay current with latest research and techniques. This section covers state-of-the-art methods essential for advanced practitioners.

|Topic|Focus & Purpose|
|---|---|
|**[[1.13.1 Prompt Chaining]]**|Sequential prompts; pipeline design; inter-prompt communication; state management; complex workflows. Multi-step processes.|
|**[[1.13.2 Automatic Prompt Engineering]]**|APE techniques; prompt optimization; evolutionary algorithms; gradient-based optimization; automated improvement. Automated optimization.|
|**[[1.13.3 Meta-Prompting]]**|Prompts about prompting; self-improvement; prompt generation; reflection on prompts; meta-level instructions. Higher-order prompting.|
|**[[1.13.4 Soft Prompting]]**|Continuous prompts; learned embeddings; prompt tuning; parameter-efficient tuning; when soft prompts help. Trainable prompts.|
|**[[1.13.5 Instruction Tuning]]**|Instruction datasets; fine-tuning for instruction following; FLAN; T0; instruction diversity. Model training.|
|**[[1.13.6 RLHF Implications]]**|Reinforcement learning from human feedback; alignment; reward modeling; preference learning; implications for prompting. Training methodology.|
|**[[1.13.7 Multimodal Prompting]]**|Text-image prompts; audio prompts; video understanding; cross-modal reasoning; multimodal future. Beyond text.|
|**[[1.13.8 Research Frontiers]]**|Latest papers; emerging techniques; future directions; experimental methods; staying current; research trends. Cutting edge.|
