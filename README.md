# Master GenAI & ML Lead Interview Study Guide

> **Structured for Visual Learners**: Every topic begins with an end-to-end **Flowchart / Architecture Diagram**, followed by a crisp breakdown of **What Each Piece Does**, key **Trade-offs**, and an **Interview "Golden Answer" Blueprint** grounded in **Azure Cloud**.

---

## 🗺️ Master Curriculum Roadmap (Mind Map)

```mermaid
mindmap
  root((GenAI & ML Lead Mastery))
    Level 1: Enterprise RAG & Ingestion
      Ingestion & Layout Parsing
        Azure AI Document Intelligence
        Table & Markdown Structure Preservation
      Parent-Child Chunking
        250-token child vectors for search
        1200-token parent context for LLM
      Hybrid Retrieval
        Dense text-embedding-3-large
        Sparse BM25 Keyword Search
        Reciprocal Rank Fusion RRF
      Enterprise Security
        Microsoft Entra ID ACL Filtering
        Zero-Trust Pre-Retrieval Pruning
    Level 2: Scale, Latency & Caching
      Performance Targets
        Sub-2s End-to-End Latency
        1000+ Concurrent Business Users
      Multi-Layer Caching Hierarchy
        L1: Exact Match In-Memory Cache
        L2: Semantic Vector Cache in Redis
        L3: Embedding & Retrieved Chunk Cache
      Serving Infrastructure
        Azure OpenAI PTU Provisioned Throughput
        FastAPI Async Orchestration on AKS
    Level 3: Hallucination Mitigation & Evals
      Hallucination Root Causes
        Parametric vs Source Conflict
        Retrieval Recall Failure
        Reasoning / Synthesis Misattribution
      Detection & Guardrails
        NLI-Based Faithfulness Verification
        Deterministic Citation Validator
        Calibrated Refusal Threshold
      Evaluation Framework
        MLflow LLM Evaluation Metrics
        Golden Ground-Truth Benchmark
    Level 4: Fine-Tuning vs RAG vs Prompting
      Decision Framework & ROI
        When to Prompt vs RAG vs Fine-Tune
        Cutting 50K per month Bill by 80%
      Query Routing Architecture
        Intent Classifier Gateway
        Category-Specific Small Model Routing
      Efficient Fine-Tuning
        LoRA Low-Rank Adaptation
        QLoRA 4-bit Quantization
        Preventing Catastrophic Forgetting
    Level 5: Context Window & KV Cache
      500-Page Document Ingestion
        Lost in the Middle Phenomenon
        Hierarchical Summarization Trees
      Inference Memory Mechanics
        KV Cache Memory Footprint Math
        PagedAttention & vLLM Architecture
        State-Space Models & Mamba
    Level 6: Multi-Agent Systems & Tools
      Orchestration & Planning
        Supervisor & Graph State Machine
        ReAct vs Tree of Thoughts
      Safety & Control Loops
        Loop Prevention via State Hashing
        Token Budget & Circuit Breaker
      Inter-Agent Consensus
        Consensus Fact-Checking
        Async Parallel Execution
    Level 7: MLOps, CI/CD & Production Triage
      MLOps Maturity Evolution
        Level 0 Notebooks to Level 3 Full Auto
        Weekly Retraining via Azure ML Pipelines
      Production Incident Triage
        Un-alerted Outage Root Cause Analysis
        Data Drift vs Concept Drift vs Infra
        Shadow Mode & Automated Rollback
    Level 8: ML Leadership & Multi-Cloud
      Engineering Leadership
        Coaching Junior ML Engineers
        Cross-Functional Alignment DS vs Eng vs Product
      Multi-Cloud Architecture
        Azure & AWS Portability
        Terraform Infrastructure as Code
```

| Level | Topic | Core Interview Question Mapped |
| :--- | :--- | :--- |
| **Level 1** | **Enterprise RAG & Permission-Aware Ingestion** | *ML Lead Q1 (500K docs, SharePoint/ACLs) & Hard GenAI Q1* |
| **Level 2** | **Scale, Low Latency (<2s) & Multi-Level Caching** | *Hard GenAI Q1 (Part C: 1000+ users, caching)* |
| **Level 3** | **Hallucination Mitigation, Evals & Guardrails** | *Hard GenAI Q3 (Medical scenario, citations, NLI)* |
| **Level 4** | **Fine-Tuning vs RAG Decision Framework & Cost Cutting** | *Hard GenAI Q2 (Reduce $50K/mo bill, LoRA/QLoRA)* |
| **Level 5** | **Context Window Management & Long-Context Processing** | *Hard GenAI Q4 (500-page filings, KV Cache, PagedAttention)* |
| **Level 6** | **Multi-Agent Systems, Tool Execution & Safety** | *Hard GenAI Q5 (Scientific research orchestrator, loops)* |
| **Level 7** | **MLOps Maturity, CI/CD & Production Incident Triage** | *ML Lead Q3, Q5, Q7, Q8 (0-to-3 maturity, Monday outage)* |
| **Level 8** | **Engineering Leadership, Mentoring & Multi-Cloud** | *ML Lead Q6, Q9, Q10 (Junior coaching, cross-cloud)* |

---

# Level 1: Enterprise RAG Architecture & Ingestion

> **Target Interview Questions:**
> - *"You're asked to build an enterprise RAG system for a company with 500K+ internal documents across SharePoint, Confluence, and PDFs with 5,000 daily queries. How do you design this end-to-end?"* (ML Lead Q1)
> - *"Design an advanced RAG retrieval pipeline across text, tables, and temporal updates."* (Hard GenAI Q1)

---

### 1.1 The Complete Architecture Flowchart

```mermaid
flowchart TD
    subgraph INGESTION["1. Document Ingestion & Indexing Pipeline (Asynchronous)"]
        SP[SharePoint / Confluence / Blob Storage] --> Event[Azure Event Grid / Blob Trigger]
        Event --> Func[Azure Functions / Ingestion Worker]
        Func --> Parse[Layout-Aware Parser: Azure AI Document Intelligence]
        
        Parse --> Chunk[Parent-Child Chunking Strategy]
        Chunk --> Meta[Metadata & ACL Enrichment\nDoc ID, Timestamp, User/Group Security IDs]
        
        Meta --> Embed[Embedding Model\nAzure OpenAI text-embedding-3-large]
        Meta --> Sparse[Sparse Tokenizer\nBM25 / SPLADE Analyzer]
        
        Embed --> PushIndex[(Azure AI Search\nVector + Keyword Index)]
        Sparse --> PushIndex
    end

    subgraph QUERY["2. User Query & Retrieval Pipeline (Real-Time)"]
        User([Enterprise User]) --> Gateway[Azure API Management\nAuth via Microsoft Entra ID]
        Gateway --> FastApp[FastAPI Orchestrator on AKS]
        
        FastApp --> SecurityFilter[Extract User Entra ID Security Token / Groups]
        FastApp --> QueryEmbed[Embed Query via text-embedding-3-large]
        
        QueryEmbed --> AISearch[Azure AI Search\nHybrid Query + Security Filter]
        SecurityFilter --> AISearch
        
        AISearch -- 1. Dense Vector KNN --> CandidatePool[Top 50 Chunks]
        AISearch -- 2. Sparse BM25 Match --> CandidatePool
        AISearch -- 3. Security ACL Pruning --> CandidatePool
        
        CandidatePool --> RRF[Reciprocal Rank Fusion - RRF]
        RRF --> Rerank[Cross-Encoder / Semantic Reranker\nTop 5 Chunks]
    end

    subgraph GENERATION["3. Context Assembly & Verification"]
        Rerank --> ContextAssembly[Inject Chunks + Strict System Prompt + Metadata]
        ContextAssembly --> LLM[Azure OpenAI GPT-4o / GPT-4o-mini]
        LLM --> Guardrail[Azure AI Content Safety & Citation Validator]
        Guardrail --> UserResponse([Final Answer with Clickable Source Citations])
    end
```

---

### 1.2 What Each Piece Does

#### A. Document Ingestion & Layout-Aware Parsing
* **The Problem:** Standard PDF text strippers mash tables, headers, and footnotes into an unreadable soup, ruining vector similarity.
* **The Solution:** Use **Azure AI Document Intelligence** (formerly Form Recognizer). It parses documents by layout, extracts markdown tables cleanly with rows/columns intact, and preserves reading order.
* **Incremental Updates:** Documents are placed in **Azure Blob Storage**. An **Azure Event Grid** trigger detects additions/modifications and fires an event so we only re-index updated documents (no full re-indexing).

#### B. Chunking Strategy: Parent-Child (Hierarchical)
* **The Problem:** Small chunks (200 tokens) are great for accurate embedding matches, but lack context for generation. Large chunks (1000 tokens) dilute embedding semantics.
* **The Solution (Parent-Child):**
  - **Child Chunks (200-300 tokens):** Indexed for semantic vector search.
  - **Parent Document/Section (1000-1500 tokens):** Stored in metadata or blob.
  - When a child chunk matches the query, we pass its **parent context** to the LLM. The LLM gets the complete picture without embedding noise.

#### C. Dual-Embedding Strategy: Dense + Sparse (Hybrid Search)
* **Dense Vectors (`text-embedding-3-large`):** Captures conceptual meaning (e.g., *"financial health"* matches *"profit margins and cash flow"*).
* **Sparse Vectors (BM25):** Captures exact keywords, part numbers, SKU codes, employee IDs, and acronyms where vector search fails.
* **Reciprocal Rank Fusion (RRF):** Combines the ranks from both search results deterministically:
  $$\text{RRF Score}(d) = \sum_{m \in \{\text{dense}, \text{sparse}\}} \frac{1}{k + \text{Rank}_m(d)} \quad (k \approx 60)$$

#### D. Enterprise Security & Access Control (Microsoft Entra ID ACLs)
* **Crucial Enterprise Concept:** If an employee isn't allowed to read the CEO's executive compensation memo on SharePoint, the RAG system must **never** return it or use it as context.
* **How It Works:** During ingestion, extract the Access Control List (ACL) from SharePoint/Confluence. Store allowed `group_ids` and `user_ids` as a filterable collection in **Azure AI Search**.
* At query time, extract the user's Entra ID claims from the bearer token and apply a hard filter:
  `search.in(user_groups, 'group1,group2')` *before* vector ranking.

#### E. Cross-Encoder Semantic Reranker
* **Why:** Vector search retrieves candidate chunks using bi-encoders (query and document embedded independently).
* **Reranker:** A cross-encoder model passes both the query and candidate chunk simultaneously through attention layers, scoring true semantic relevance. Reduces top 50 candidates down to the top 5 highest-signal chunks.

---

### 1.3 Key Architectural Trade-Offs

| Decision | Option A | Option B | Why We Choose Option B for Enterprise |
| :--- | :--- | :--- | :--- |
| **Search Type** | Dense Vector Only | Hybrid (Dense + BM25) + RRF | Pure vector search fails on product SKUs, acronyms, and names. Hybrid is mandatory. |
| **Chunking** | Fixed-size (500 tokens) | Parent-Child (Hierarchical) | Fixed-size splits sentences and loses context. Parent-child gives precise search + broad generation context. |
| **Access Control** | Post-filtering (filter LLM output) | Pre-filtering (filter in Search Index via ACLs) | Post-filtering leaks data, wastes tokens, and violates enterprise compliance. Pre-filtering is secure and fast. |
| **Embedding Dims** | 1536 dims | 3072 dims (reduced via Matryoshka) | Azure `text-embedding-3-large` supports Matryoshka embeddings (truncate to 1024 or 1536 without loss) to cut storage by 50%. |

---

### 1.4 The 3-Minute Interview "Golden Answer" Script

When the interviewer asks: **"How do you design an enterprise RAG system for 500K documents with permissions?"**

> **1. Framing & Requirements (30s):**
> *"I treat enterprise RAG as three distinct subsystems: An asynchronous secure ingestion pipeline, a hybrid retrieval engine with permission pre-filtering, and an observable generation layer with guardrails."*
>
> **2. Ingestion & Security (60s):**
> *"For 500K documents across SharePoint and Confluence, documents flow into Azure Blob Storage with Azure Event Grid triggers for incremental updates. We parse them with layout-aware parsers (Azure AI Document Intelligence) to preserve tables and headers.
> Critically, during ingestion, we extract the document's Entra ID Access Control List (ACL) and store allowed user/group IDs in Azure AI Search. We use parent-child chunking: 250-token child chunks for vector indexing, mapped to 1200-token parent sections."*
>
> **3. Retrieval & Serving (60s):**
> *"At query time, the user authenticates via Microsoft Entra ID through Azure API Management. We extract their security groups and issue a hybrid search in Azure AI Search combining dense embeddings (`text-embedding-3-large`) and sparse BM25, pre-filtered by their security IDs.
> We combine results using Reciprocal Rank Fusion (RRF), run the top 50 candidates through Azure AI Search's Semantic Reranker down to top 5, and assemble the parent context."*
>
> **4. Generation & Observability (30s):**
> *"The context is passed to Azure OpenAI GPT-4o with strict citation formatting and an explicit refusal prompt if confidence is low. We run Azure AI Content Safety and log inputs, latency, and faithfulness scores via MLflow to catch drift."*

---
