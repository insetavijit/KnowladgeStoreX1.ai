### **[[4.1 Text Processing Fundamentals]]**

Master foundational text processing techniques essential for all NLP applications. Learn tokenization, normalization, cleaning, and preprocessing pipelines. Understand encoding, decoding, and character-level operations. Build robust text processing systems that handle real-world data. Text processing is the first step in every NLP pipeline—poor preprocessing leads to degraded model performance. This foundation enables all downstream NLP tasks.

| Topic                                  | Focus & Purpose                                                                                                                                                          |
| -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **[[4.1.1 Tokenization Basics]]**      | Word tokenization; sentence tokenization; whitespace splitting; punctuation handling; tokenization challenges; language-specific tokenization. Breaking text into units. |
| **[[4.1.2 Text Normalization]]**       | Lowercasing; case folding; Unicode normalization; accent removal; text standardization; consistency. Standardizing text.                                                 |
| **[[4.1.3 Text Cleaning]]**            | Removing noise; HTML stripping; special character handling; whitespace normalization; data quality; cleaning pipelines. Preparing clean text.                            |
| **[[4.1.4 Stop Words]]**               | Stop word lists; stop word removal; when to keep stop words; custom stop words; language-specific; impact on models. Filtering common words.                             |
| **[[4.1.5 Stemming & Lemmatization]]** | Porter stemmer; Lancaster stemmer; Snowball stemmer; lemmatization; morphological analysis; trade-offs; when to use. Word normalization.                                 |
| **[[4.1.6 Regular Expressions]]**      | Regex syntax; pattern matching; text extraction; regex for NLP; common patterns; regex optimization. Pattern-based processing.                                           |
| **[[4.1.7 Encoding & Unicode]]**       | Character encoding; UTF-8; Unicode handling; encoding errors; decoding; multilingual text. Text representation.                                                          |
| **[[4.1.8 Preprocessing Pipelines]]**  | Chaining operations; pipeline design; spaCy pipelines; NLTK pipelines; custom pipelines; reusable preprocessing. End-to-end processing.                                  |

### **[[4.2 Advanced Tokenization]]**

Master modern tokenization approaches essential for transformers and LLMs. Learn subword tokenization, BPE, WordPiece, SentencePiece, and tokenizer training. Understand vocabulary construction, special tokens, and tokenization for different languages. Modern LLMs rely on subword tokenization—understanding this is critical for working with language models effectively.

| Topic                                   | Focus & Purpose                                                                                                                                    |
| --------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| **[[4.2.1 Subword Tokenization]]**      | Subword units; advantages; OOV handling; morphology capture; vocabulary efficiency; subword segmentation. Modern tokenization.                     |
| **[[4.2.2 Byte-Pair Encoding (BPE)]]**  | BPE algorithm; merge operations; vocabulary building; GPT tokenization; BPE variants; implementation. Compression-based tokenization.              |
| **[[4.2.3 WordPiece]]**                 | WordPiece algorithm; BERT tokenization; likelihood-based merging; WordPiece vs BPE; Google's approach. BERT-family tokenization.                   |
| **[[4.2.4 SentencePiece]]**             | Language-agnostic tokenization; unsupervised training; unigram LM; SentencePiece models; multilingual; raw text input. Universal tokenization.     |
| **[[4.2.5 Tokenizer Training]]**        | Training custom tokenizers; vocabulary size selection; training corpus; special tokens; tokenizer configuration. Building tokenizers.              |
| **[[4.2.6 Special Tokens]]**            | [CLS], [SEP], [PAD], [UNK], [MASK]; special token handling; positional encoding; token type IDs; attention masks. Model-specific tokens.           |
| **[[4.2.7 Multilingual Tokenization]]** | Cross-lingual tokenization; shared vocabularies; language detection; script handling; Unicode ranges. Global NLP.                                  |
| **[[4.2.8 Tokenization for LLMs]]**     | HuggingFace tokenizers; GPT-4 tokenization; Claude tokenization; token counting; tokenization debugging; fast tokenizers. Production tokenization. |

### **[[4.3 Word Embeddings]]**

Master word embeddings as fundamental representations for NLP. Learn Word2Vec, GloVe, FastText, and embedding properties. Understand training embeddings, similarity computation, and embedding evaluation. Use pre-trained embeddings and fine-tune for domains. Embeddings are the bridge from discrete words to continuous representations—essential foundation for modern NLP.

| Topic                                 | Focus & Purpose                                                                                                                                 |
| ------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| **[[4.3.1 Embedding Concepts]]**      | Distributed representations; vector semantics; dimensionality; embedding space; geometric properties. Foundational concepts.                    |
| **[[4.3.2 Word2Vec]]**                | Skip-gram; CBOW; negative sampling; hierarchical softmax; training Word2Vec; implementation; hyperparameters. Classic embeddings.               |
| **[[4.3.3 GloVe]]**                   | Global vectors; co-occurrence matrix; matrix factorization; GloVe objectives; training GloVe; comparison to Word2Vec. Count-based embeddings.   |
| **[[4.3.4 FastText]]**                | Subword embeddings; character n-grams; OOV handling; FastText training; morphology; language models. Robust embeddings.                         |
| **[[4.3.5 Embedding Properties]]**    | Semantic similarity; analogies; bias in embeddings; embedding evaluation; intrinsic evaluation; extrinsic evaluation. Understanding embeddings. |
| **[[4.3.6 Pre-trained Embeddings]]**  | Loading embeddings; GloVe files; Word2Vec format; Gensim; embedding libraries; model selection. Using existing embeddings.                      |
| **[[4.3.7 Domain Adaptation]]**       | Fine-tuning embeddings; domain-specific embeddings; updating embeddings; specialized vocabularies. Custom embeddings.                           |
| **[[4.3.8 Embedding Visualization]]** | t-SNE; UMAP; PCA; embedding plots; cluster visualization; interpretation. Understanding representations.                                        |

### **[[4.4 Contextual Embeddings & Transformers]]**

Master contextual embeddings from transformer models. Learn BERT, GPT, T5, and their architectures. Understand attention mechanisms, positional encoding, and layer representations. Extract and use embeddings from pre-trained models. Contextual embeddings revolutionized NLP—they capture meaning based on context, not just word identity.

| Topic                                  | Focus & Purpose                                                                                                                                |
| -------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| **[[4.4.1 Transformer Architecture]]** | Self-attention; multi-head attention; feedforward layers; layer normalization; residual connections; architecture overview. Core architecture. |
| **[[4.4.2 BERT Embeddings]]**          | Bidirectional encoding; [CLS] token; pooling strategies; layer selection; BERT variants (RoBERTa, ALBERT); extraction. Encoder embeddings.     |
| **[[4.4.3 GPT Embeddings]]**           | Autoregressive encoding; causal attention; GPT-2, GPT-3; decoder-only architecture; generation vs understanding. Decoder embeddings.           |
| **[[4.4.4 Sentence Embeddings]]**      | Sentence-BERT; pooling methods; mean pooling; CLS pooling; semantic similarity; sentence transformers. Text-level representations.             |
| **[[4.4.5 Cross-lingual Embeddings]]** | Multilingual BERT; XLM-RoBERTa; mBERT; zero-shot cross-lingual; alignment; translation-free NLP. Global representations.                       |
| **[[4.4.6 Domain-Specific Models]]**   | BioBERT; SciBERT; FinBERT; LegalBERT; domain adaptation; specialized vocabularies. Vertical NLP.                                               |
| **[[4.4.7 Embedding Extraction]]**     | HuggingFace transformers; layer selection; aggregation strategies; batch processing; efficient extraction. Practical usage.                    |
| **[[4.4.8 Fine-tuning Strategies]]**   | Fine-tuning vs feature extraction; learning rates; freezing layers; adapter layers; LoRA; efficient fine-tuning. Adaptation techniques.        |

### **[[4.5 Named Entity Recognition (NER)]]**

Master identifying and classifying named entities in text. Learn rule-based NER, statistical NER, neural NER, and custom entity extraction. Understand entity types, evaluation metrics, and real-world applications. Build production NER systems for information extraction. NER is fundamental for information extraction, knowledge graphs, and document understanding.

| Topic                            | Focus & Purpose                                                                                                                  |
| -------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| **[[4.5.1 NER Fundamentals]]**   | Entity types (PERSON, ORG, LOC, DATE); IOB tagging; BILOU scheme; entity boundaries; nested entities. Core concepts.             |
| **[[4.5.2 Rule-Based NER]]**     | Regular expressions; gazetteers; pattern matching; rule systems; SpaCy EntityRuler; deterministic extraction. Pattern-based NER. |
| **[[4.5.3 Statistical NER]]**    | CRF (Conditional Random Fields); sequence labeling; feature engineering; MaxEnt models; structured prediction. Classical NER.    |
| **[[4.5.4 Neural NER]]**         | LSTM-CRF; BERT for NER; token classification; BiLSTM; transformers; modern approaches. Deep learning NER.                        |
| **[[4.5.5 Custom NER]]**         | Training custom models; annotation; labeled data; Prodigy; Label Studio; active learning. Building domain NER.                   |
| **[[4.5.6 Evaluation Metrics]]** | Precision, recall, F1; entity-level evaluation; token-level evaluation; strict vs partial matching. Measuring performance.       |
| **[[4.5.7 Entity Linking]]**     | Linking to knowledge bases; disambiguation; Wikidata; DBpedia; entity normalization. Connecting entities.                        |
| **[[4.5.8 Production NER]]**     | SpaCy NER; HuggingFace NER; API services; error handling; post-processing; confidence thresholding. Deployed systems.            |

### **[[4.6 Part-of-Speech Tagging & Parsing]]**

Master syntactic analysis of text through POS tagging and parsing. Learn dependency parsing, constituency parsing, and syntactic features. Understand parse trees, grammatical relations, and syntax-based features. Build systems that understand grammatical structure. Syntax provides crucial information for many NLP tasks including information extraction and question answering.

| Topic                               | Focus & Purpose                                                                                                                |
| ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| **[[4.6.1 POS Tagging Basics]]**    | Penn Treebank tags; universal POS tags; tag sets; tagging accuracy; ambiguity; POS usage. Grammatical categories.              |
| **[[4.6.2 POS Tagging Methods]]**   | HMM tagging; CRF tagging; neural tagging; BERT POS tagging; SpaCy; NLTK. Tagging approaches.                                   |
| **[[4.6.3 Dependency Parsing]]**    | Dependency relations; dependency trees; universal dependencies; typed dependencies; parsing algorithms. Grammatical structure. |
| **[[4.6.4 Constituency Parsing]]**  | Parse trees; phrase structure; CFG; constituent analysis; tree banks; nested structure. Hierarchical syntax.                   |
| **[[4.6.5 Parsing Algorithms]]**    | Shift-reduce; transition-based; graph-based; neural parsing; efficient parsing. Computational methods.                         |
| **[[4.6.6 Syntax-Based Features]]** | Extracting syntactic features; parse tree features; path features; syntax for downstream tasks. Using syntax.                  |
| **[[4.6.7 Error Analysis]]**        | Parse errors; attachment ambiguity; difficult constructions; evaluation; improving accuracy. Understanding failures.           |
| **[[4.6.8 Production Parsing]]**    | SpaCy parser; Stanza; CoreNLP; parsing pipelines; speed-accuracy trade-offs. Deployed parsers.                                 |

### **[[4.7 Text Classification]]**

Master classifying text into categories using traditional and modern approaches. Learn feature extraction, classical ML, neural classifiers, and fine-tuned transformers. Build sentiment analysis, topic classification, and intent detection systems. Text classification is one of the most common NLP tasks—essential for production applications.

| Topic                                 | Focus & Purpose                                                                                                    |
| ------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| **[[4.7.1 Classification Basics]]**   | Problem formulation; labels; training data; evaluation; multi-class; multi-label. Core concepts.                   |
| **[[4.7.2 Feature Engineering]]**     | Bag-of-words; TF-IDF; n-grams; feature selection; feature extraction; representation. Traditional features.        |
| **[[4.7.3 Classical Classifiers]]**   | Naive Bayes; Logistic Regression; SVM; Random Forests; ensemble methods; scikit-learn. ML algorithms.              |
| **[[4.7.4 Neural Classifiers]]**      | CNN for text; LSTM; BiLSTM; attention; text classification architectures. Deep learning classifiers.               |
| **[[4.7.5 Transformer Classifiers]]** | Fine-tuning BERT; GPT classification; RoBERTa; sequence classification; classification head. Modern classifiers.   |
| **[[4.7.6 Sentiment Analysis]]**      | Polarity detection; emotion classification; aspect-based sentiment; fine-grained sentiment. Opinion mining.        |
| **[[4.7.7 Topic Classification]]**    | Topic modeling; document categorization; news classification; hierarchical classification. Content categorization. |
| **[[4.7.8 Few-Shot & Zero-Shot]]**    | Low-resource classification; prompt-based; in-context learning; data augmentation. Limited data scenarios.         |

### **[[4.8 Information Extraction]]**

Master extracting structured information from unstructured text. Learn relation extraction, event extraction, and knowledge base construction. Build systems that convert text to structured data, populate databases, and create knowledge graphs. Information extraction bridges NLP and structured data—critical for enterprise applications.

| Topic                                     | Focus & Purpose                                                                                                      |
| ----------------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| **[[4.8.1 Relation Extraction]]**         | Binary relations; subject-predicate-object; relation classification; distant supervision. Finding relationships.     |
| **[[4.8.2 Event Extraction]]**            | Event detection; event arguments; temporal events; event schemas; ACE; event structure. Capturing events.            |
| **[[4.8.3 Coreference Resolution]]**      | Mention detection; coreference chains; entity linking; anaphora resolution; pronoun resolution. Connecting mentions. |
| **[[4.8.4 Slot Filling]]**                | Template filling; slot extraction; form understanding; structured extraction. Filling templates.                     |
| **[[4.8.5 Open Information Extraction]]** | Unsupervised extraction; triple extraction; ClausIE; OpenIE; relation discovery. Schema-free extraction.             |
| **[[4.8.6 Knowledge Base Population]]**   | KB construction; entity resolution; knowledge graphs; Neo4j; graph databases. Building knowledge.                    |
| **[[4.8.7 Temporal Information]]**        | Time expressions; temporal relations; event ordering; TimeML; temporal reasoning. Understanding time.                |
| **[[4.8.8 Evaluation & Metrics]]**        | Precision, recall; extraction metrics; error analysis; quality assessment. Measuring extraction.                     |

### **[[4.9 Language Modeling]]**

Master language modeling from n-grams to neural models. Learn statistical LMs, neural LMs, and transformer LMs. Understand perplexity, evaluation, and text generation. Build language models and understand LLM foundations. Language modeling is the core task that powers modern LLMs—understanding LM fundamentals is essential.

| Topic                                     | Focus & Purpose                                                                                             |
| ----------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| **[[4.9.1 N-gram Models]]**               | Unigrams, bigrams, trigrams; smoothing; backoff; interpolation; n-gram probability. Classical LMs.          |
| **[[4.9.2 Neural Language Models]]**      | RNN LMs; LSTM LMs; perplexity; training LMs; next token prediction. Neural LMs.                             |
| **[[4.9.3 Transformer Language Models]]** | GPT architecture; causal attention; autoregressive LMs; decoder-only; scaling laws. Modern LMs.             |
| **[[4.9.4 Masked Language Models]]**      | BERT pre-training; masked token prediction; bidirectional context; MLM objective. Encoder LMs.              |
| **[[4.9.5 Perplexity & Evaluation]]**     | Perplexity metric; evaluation sets; cross-entropy; bits-per-character; model comparison. Measuring quality. |
| **[[4.9.6 Text Generation]]**             | Sampling strategies; temperature; top-k; top-p (nucleus); beam search; generation quality. Generating text. |
| **[[4.9.7 Conditional Generation]]**      | Seq2seq; encoder-decoder; conditional LMs; controlled generation; style transfer. Task-specific generation. |
| **[[4.9.8 Domain Language Models]]**      | Domain adaptation; specialized LMs; medical LMs; code LMs; legal LMs. Vertical LMs.                         |

### **[[4.10 Sequence-to-Sequence Models]]**

Master seq2seq architectures for generation tasks. Learn machine translation, summarization, and generation patterns. Understand encoder-decoder architectures, attention mechanisms, and beam search. Build translation and summarization systems. Seq2seq is foundational for many generation tasks and understanding modern LLMs.

| Topic                                     | Focus & Purpose                                                                                                |
| ----------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| **[[4.10.1 Seq2seq Basics]]**             | Encoder-decoder; sequence transduction; RNN seq2seq; architecture overview. Core architecture.                 |
| **[[4.10.2 Attention Mechanisms]]**       | Attention scores; alignment; Bahdanau attention; Luong attention; attention visualization. Focusing mechanism. |
| **[[4.10.3 Transformer Seq2seq]]**        | T5; BART; mT5; encoder-decoder transformers; modern architectures. Transformer generation.                     |
| **[[4.10.4 Machine Translation]]**        | NMT; translation systems; BLEU score; translation evaluation; multilingual models. Language translation.       |
| **[[4.10.5 Text Summarization]]**         | Extractive summarization; abstractive summarization; ROUGE scores; summarization models. Content condensation. |
| **[[4.10.6 Decoding Strategies]]**        | Greedy decoding; beam search; diverse beam search; sampling; length normalization. Generation control.         |
| **[[4.10.7 Evaluation Metrics]]**         | BLEU; ROUGE; METEOR; BERTScore; human evaluation; automatic metrics. Quality measurement.                      |
| **[[4.10.8 Fine-tuning for Generation]]** | Fine-tuning T5/BART; task-specific generation; optimization; generation quality. Adaptation.                   |

### **[[4.11 Question Answering]]**

Master building question answering systems from extractive to generative approaches. Learn reading comprehension, open-domain QA, and conversational QA. Understand answer extraction, ranking, and generation. Build production QA systems for customer support and information retrieval. QA is a key application combining retrieval, NLP, and generation.

| Topic                                | Focus & Purpose                                                                                              |
| ------------------------------------ | ------------------------------------------------------------------------------------------------------------ |
| **[[4.11.1 QA Task Types]]**         | Extractive QA; abstractive QA; multiple choice; open-domain; closed-domain; conversational QA. QA varieties. |
| **[[4.11.2 Extractive QA]]**         | Span extraction; SQuAD; answer start/end; BERT QA; context-based QA. Finding answers.                        |
| **[[4.11.3 Reading Comprehension]]** | MRC tasks; comprehension models; context understanding; inference; reasoning. Understanding text.            |
| **[[4.11.4 Open-Domain QA]]**        | Retriever-reader; DPR; REALM; open-book QA; knowledge-intensive QA. Large-scale QA.                          |
| **[[4.11.5 Generative QA]]**         | Seq2seq QA; RAG; FiD; generation-based answers; natural answers. Generating answers.                         |
| **[[4.11.6 Conversational QA]]**     | Multi-turn QA; context tracking; conversational context; follow-up questions. Dialogue-based QA.             |
| **[[4.11.7 Answer Ranking]]**        | Candidate ranking; answer scoring; reranking; confidence estimation. Selecting answers.                      |
| **[[4.11.8 QA Evaluation]]**         | Exact match; F1 score; answer quality; human evaluation; error analysis. Measuring performance.              |

### **[[4.12 Advanced NLP Topics]]**

Master cutting-edge NLP techniques and specialized topics. Learn multimodal NLP, cross-lingual methods, low-resource NLP, and interpretability. Understand bias detection, fairness, and ethical considerations. Build sophisticated NLP systems with state-of-the-art techniques. This section covers expert-level topics for advanced practitioners.

| Topic                            | Focus & Purpose                                                                                                          |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| **[[4.12.1 Multimodal NLP]]**    | Vision-language; image captioning; VQA; CLIP; multimodal transformers; cross-modal understanding. Beyond text.           |
| **[[4.12.2 Cross-lingual NLP]]** | Multilingual models; zero-shot transfer; cross-lingual embeddings; machine translation; language universals. Global NLP. |
| **[[4.12.3 Low-Resource NLP]]**  | Few-shot learning; data augmentation; transfer learning; multilingual transfer; synthetic data. Limited data.            |
| **[[4.12.4 Interpretability]]**  | Attention visualization; LIME; SHAP; saliency maps; explaining predictions; model probing. Understanding models.         |
| **[[4.12.5 Bias & Fairness]]**   | Detecting bias; gender bias; racial bias; fairness metrics; debiasing; ethical NLP. Responsible NLP.                     |
| **[[4.12.6 Domain Adaptation]]** | Transfer learning; fine-tuning; domain shift; adaptation techniques; multi-domain. Specialization.                       |
| **[[4.12.7 Efficient NLP]]**     | Model compression; distillation; quantization; pruning; efficient transformers; mobile NLP. Resource optimization.       |
| **[[4.12.8 NLP for Code]]**      | Code understanding; code generation; CodeBERT; Codex; program synthesis; code search. Programming language processing.   |

---
