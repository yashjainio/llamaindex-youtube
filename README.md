# **LlamaIndex RAG Series**

Welcome to the **LlamaIndex RAG Series** repository!

This series is designed to help you understand Retrieval-Augmented Generation with **LlamaIndex** from the ground up — starting with why LlamaIndex exists and how `VectorStoreIndex` works, all the way to advanced topics like hybrid search, reranking, GraphRAG (`PropertyGraphIndex`), native agents (`FunctionAgent`), observability, and evaluation.
Each episode is a self-contained notebook that walks through real, working code against the same small shared dataset, so you can build production-ready RAG applications that answer questions grounded in your own data.

---

## 🐍 **Install Python Using Miniconda / Miniforge**

To keep your AI projects clean and organized, it is recommended to use **conda environments**. Follow the steps below to install Miniforge and set up your environment.

---

### 🔗 **Download Miniforge for macOS (ARM64)**

Download from the official repository:  
https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-MacOSX-arm64.sh

---

### 💻 **Install Miniforge**

Run the following commands:

```bash
chmod +x ~/Downloads/Miniforge3-MacOSX-arm64.sh
sh ~/Downloads/Miniforge3-MacOSX-arm64.sh
source ~/miniforge3/bin/activate
```

---

### 🧱 **Create the project's conda environment**

All packages for this repo are installed inside a single project-local environment, `.llama-index-youtube-env`:

```bash
conda create --prefix ./.llama-index-youtube-env python=3.12
conda activate ./.llama-index-youtube-env
```

---

### 📦 **Install packages from requirements.txt**

```bash
pip install -r requirements.txt
```

---

### 🔑 **Set up your API keys**

Create a `.env` file in the project root with your provider keys (e.g. `OPENAI_API_KEY=...`). Every notebook loads it automatically via `python-dotenv`'s `load_dotenv()` — nothing else to configure.

Your LlamaIndex RAG environment is ready to build powerful AI apps 🚀

---

# **📺 Series Breakdown**

### **1. What is LlamaIndex?**

- What LlamaIndex is built for and how it differs from LangChain/LangGraph as a retrieval layer vs. an orchestration layer.
- Building a full load → index → query RAG pipeline in a handful of lines with `VectorStoreIndex`.

### **2. VectorStoreIndex — Your First RAG Pipeline**

- Walking documents → nodes → index → query engine step by step with `SimpleDirectoryReader` and `VectorStoreIndex.from_documents()`.
- Understanding exactly what `index.as_query_engine()` wires together under the hood.

### **3. Nodes & Documents**

- Building a `Document` by hand and splitting it into `Node`s manually with `SentenceSplitter`.
- Seeing how `chunk_size` and overlap trade-offs change the resulting Nodes.

### **4. Query Engines**

- Tuning `similarity_top_k` to control how many chunks get retrieved per query.
- Comparing `response_mode` strategies like `compact` vs. `tree_summarize` for answer synthesis.

### **5. RouterQueryEngine**

- Wrapping multiple indices (`VectorStoreIndex`, `SummaryIndex`) as `QueryEngineTool`s with descriptions.
- Letting an `LLMSingleSelector` route each question to the right tool automatically.

### **6. Metadata Filtering**

- Attaching custom metadata to documents so it carries through to every node created from them.
- Filtering retrieval to a metadata subset before semantic search runs.

### **7. Hybrid Search**

- Combining a BM25 keyword retriever with vector search via reciprocal rank fusion.
- Comparing hybrid vs. vector-only results on exact, keyword-friendly questions.

### **8. PDF Parsing**

- Parsing complex, table-heavy PDFs locally and offline with `pymupdf4llm`.
- Comparing it against a basic `SimpleDirectoryReader` extraction of the same file.

### **9. Persisting Indexes & Vector Stores**

- Persisting the default in-memory index to disk with `storage_context.persist()` / `load_index_from_storage()`.
- Swapping in a Chroma vector store for automatic, production-style persistence.

### **10. Reranking for Better Retrieval**

- Retrieving a wide candidate set cheaply with embedding similarity.
- Re-scoring those candidates locally with a `SentenceTransformerRerank` cross-encoder.

### **11. Chat Engines & Memory**

- Adding a `ChatMemoryBuffer` on top of an index so follow-up questions resolve using prior turns.
- Inspecting exactly what `condense_plus_context` stores and reuses between turns.

### **12. Structured Outputs with Pydantic**

- Forcing LLM output into a typed Pydantic model with `as_structured_llm()`.
- Seeing how field descriptions directly shape extraction accuracy.

### **13. Ingestion Pipeline & Incremental Updates**

- Building an `IngestionPipeline` backed by a docstore and a Chroma vector store.
- Running it twice to see already-processed documents get skipped and new ones picked up.

### **14. Sub-Question Query Engine & Multi-Document Agents**

- Giving each document its own index and `QueryEngineTool` instead of one shared index.
- Using `SubQuestionQueryEngine` to break a cross-document question into per-tool sub-questions.

### **15. Multi-Modal RAG**

- Feeding a vision-capable LLM an image directly alongside text via an `ImageBlock`.
- Chaining an image-derived answer into a follow-up text query against the existing corpus.

### **16. Property Graph Index (GraphRAG)**

- Extracting entity → relationship → entity triplets from documents with `PropertyGraphIndex`.
- Querying the resulting graph for relationship questions vector search alone can't chain together.

### **17. Evaluating RAG**

- Scoring answers for faithfulness and relevancy without needing a ground-truth reference.
- Scoring correctness against a known reference answer with a dedicated evaluator LLM.

### **18. AgentWorkflow & FunctionAgent**

- Wrapping retrieval as a `FunctionTool` an agent can choose to call.
- Building a `FunctionAgent` that decides per-question whether to call that tool at all — no LangChain/LangGraph involved.

### **19. Observability & Tracing with Arize Phoenix**

- Instrumenting LlamaIndex with OpenTelemetry via `LlamaIndexInstrumentor` to trace every internal step.
- Pulling captured traces back programmatically as a dataframe from the Phoenix client.

---

# **📄 requirements.txt**

```
# Install via: conda activate ./.llama-index-youtube-env && pip install -r requirements.txt
llama-index
llama-index-core
llama-index-readers-file
python-dotenv
ipykernel
llama-index-retrievers-bm25
PyStemmer
llama-cloud
pymupdf4llm
langgraph
langchain-openai
langchain-core
chromadb
llama-index-vector-stores-chroma
sentence-transformers
matplotlib
arize-phoenix
openinference-instrumentation-llama-index
```

---

# **📂 data/**

Shared sample data used across every episode, so no notebook needs an earlier one to have been run first:

- `data/sample_docs/` — five short anime-overview `.txt` files (`naruto`, `demon_slayer`, `dragon_ball`, `death_note`, `solo_leveling`) used as the default text corpus.
- `data/sample.pdf` — a table-heavy PDF used in the PDF parsing episode.

---

# **🤝 Contributing**

Got suggestions or improvements?  
Feel free to open an issue or submit a pull request.

---

# **📬 Stay Connected**

- [YouTube Channel](https://www.youtube.com/@yashjainio)
- [LinkedIn](https://www.linkedin.com/in/yashjainio)

---

Thank you for checking out the **LlamaIndex RAG Series**!  
Happy building with AI 🚀
