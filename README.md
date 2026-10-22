
# AI Document Intelligence Platform

> **Production-oriented RAG system for intelligent document search and question answering**

## 📌 Overview

This project aims to design and deploy a production-oriented **AI Document Intelligence Platform** capable of understanding enterprise documents and answering user questions with **reliable, contextualized and cited responses**.

The system combines **Retrieval-Augmented Generation (RAG)**, semantic search, hybrid retrieval, reranking, LLMs and automated evaluation.

The main objective is not only to build a functional chatbot, but to study and optimize the complete AI pipeline:

**Data → Retrieval → Generation → Evaluation → Deployment → Monitoring**

---

## 🎯 Objectives

The project focuses on five main objectives:

- Build a complete RAG pipeline from document ingestion to answer generation.
- Compare different retrieval and embedding strategies.
- Evaluate the quality and reliability of generated answers.
- Optimize the system for **accuracy, latency and cost**.
- Deploy the solution as a production-ready API.

---

# 🏗️ System Architecture

```text
                         ┌──────────────────┐
                         │    Documents     │
                         │ PDF / DOCX / TXT │
                         └────────┬─────────┘
                                  │
                                  ▼
                         ┌──────────────────┐
                         │ Document Parser  │
                         └────────┬─────────┘
                                  │
                                  ▼
                         ┌──────────────────┐
                         │    Chunking      │
                         └────────┬─────────┘
                                  │
                    ┌─────────────┴─────────────┐
                    ▼                           ▼
           ┌─────────────────┐         ┌─────────────────┐
           │ Dense Embedding │         │   BM25 Search   │
           └────────┬────────┘         └────────┬────────┘
                    │                           │
                    └─────────────┬─────────────┘
                                  ▼
                         ┌──────────────────┐
                         │ Hybrid Retrieval │
                         └────────┬─────────┘
                                  │
                                  ▼
                         ┌──────────────────┐
                         │     Reranker     │
                         └────────┬─────────┘
                                  │
                                  ▼
                         ┌──────────────────┐
                         │       LLM        │
                         └────────┬─────────┘
                                  │
                                  ▼
                    ┌──────────────────────────┐
                    │ Answer + Source Citations│
                    └────────────┬─────────────┘
                                 │
                  ┌──────────────┴──────────────┐
                  ▼                             ▼
          ┌─────────────────┐          ┌─────────────────┐
          │   Evaluation    │          │    Monitoring   │
          │      RAGAS      │          │ Prometheus /    │
          │                 │          │ LangSmith       │
          └─────────────────┘          └─────────────────┘
```

---

# 🚀 Main Features

## 1. Document ingestion

The platform supports multiple document formats:

- PDF
- DOCX
- TXT

Documents are automatically processed, cleaned and divided into meaningful chunks.

---

## 2. Semantic Search

Documents are converted into vector representations using embedding models.

The project will compare several embedding models to study the trade-off between:

- Retrieval quality
- Latency
- Memory usage
- Computational cost

---

## 3. Hybrid Retrieval

Instead of relying exclusively on vector search, the system combines:

### Dense retrieval

Semantic similarity using embeddings.

### Sparse retrieval

Keyword-based search using BM25.

The goal is to determine whether combining both approaches improves retrieval performance.

---

## 4. Reranking

Retrieved documents are passed through a reranking model to identify the most relevant contexts before sending them to the LLM.

This allows the project to study the impact of reranking on:

- Context relevance
- Answer quality
- Latency

---

# 🤖 LLM Generation

The selected contexts are provided to an LLM together with the user's question.

The model generates:

- A natural-language answer
- Relevant document citations
- A confidence/reliability signal when possible

The system is designed to reduce hallucinations by forcing the model to rely on retrieved information.

---

# 📊 AI Evaluation

A major objective of this project is to **measure the quality of the AI system rather than relying only on subjective evaluation**.

A dedicated evaluation dataset will contain:

```text
Question
Expected Answer
Relevant Documents
```

The following metrics will be investigated:

- Context Precision
- Context Recall
- Answer Relevancy
- Faithfulness
- Retrieval Recall
- End-to-End Latency

Example experiment:

| Configuration | Retrieval Recall | Faithfulness | Latency |
|---|---:|---:|---:|
| Embedding A | 78% | 82% | 0.8s |
| Embedding B | 84% | 87% | 1.1s |
| Embedding C | 86% | 89% | 1.8s |

The objective is to identify the best configuration according to the application's requirements.

---

# ⚡ Performance Optimization

The project will investigate several optimization techniques:

- Chunk size optimization
- Overlap optimization
- Embedding model selection
- Top-K retrieval optimization
- Reranking
- LLM selection
- Quantization
- Caching
- Batch inference

Performance will be measured using:

```text
Accuracy
Latency
Throughput
Memory consumption
Cost per request
```

---

# 🧪 Experiment Tracking

Experiments will be tracked using **MLflow**.

Each experiment can record:

```text
Model
Embedding model
Chunk size
Top-K
Reranker
Evaluation metrics
Latency
```

This makes it possible to compare different versions of the system and reproduce experiments.

---

# 🌐 API

The application exposes a REST API using **FastAPI**.

Example endpoint:

```http
POST /ask
```

Request:

```json
{
  "question": "What is the company's revenue for 2025?"
}
```

Response:

```json
{
  "answer": "The company's revenue for 2025 was ...",
  "sources": [
    {
      "document": "annual_report_2025.pdf",
      "page": 42
    }
  ]
}
```

---

# 🐳 Deployment

The application is containerized using **Docker**.

The target deployment architecture is:

```text
GitHub
   │
   ▼
CI/CD Pipeline
   │
   ▼
Docker Image
   │
   ▼
Cloud Infrastructure
   │
   ├── FastAPI
   ├── Vector Database
   ├── LLM
   └── Monitoring
```

---

# 📈 Monitoring

The production system will monitor:

### Application metrics

- Request latency
- Requests per second
- Error rate
- API availability

### AI metrics

- Retrieval quality
- Answer relevance
- Hallucination rate
- Token usage
- Model latency

The objective is to detect both **technical failures and AI-quality degradation**.

---

# 🧰 Tech Stack

### Programming

- Python
- SQL

### AI / ML

- PyTorch
- Hugging Face Transformers
- Sentence Transformers
- LLMs
- RAG
- Embeddings
- Reranking

### Retrieval

- BM25
- Vector Search
- ChromaDB / Qdrant / PostgreSQL + pgvector

### Backend

- FastAPI
- Pydantic

### MLOps

- MLflow
- Docker
- GitHub Actions
- CI/CD

### Evaluation

- RAGAS
- Custom evaluation dataset

### Monitoring

- Prometheus
- LangSmith

### Cloud

- AWS / Azure / GCP

---

# 📁 Project Structure

```text
ai-document-intelligence/
│
├── app/
│   ├── api/
│   ├── ingestion/
│   ├── retrieval/
│   ├── embeddings/
│   ├── reranking/
│   ├── generation/
│   └── evaluation/
│
├── data/
│   ├── raw/
│   ├── processed/
│   └── evaluation/
│
├── experiments/
│   ├── embeddings/
│   ├── retrieval/
│   └── models/
│
├── tests/
│
├── notebooks/
│
├── docker/
│
├── configs/
│
├── requirements.txt
├── Dockerfile
├── docker-compose.yml
├── README.md
└── .github/
    └── workflows/
        └── ci.yml
```

---

# 🗺️ Roadmap

## Phase 1 — Baseline RAG

- [ ] Document ingestion
- [ ] Text extraction
- [ ] Chunking
- [ ] Embeddings
- [ ] Vector database
- [ ] Basic retrieval
- [ ] LLM generation

## Phase 2 — Advanced Retrieval

- [ ] BM25
- [ ] Hybrid search
- [ ] Reranking
- [ ] Retrieval benchmarking

## Phase 3 — Evaluation

- [ ] Evaluation dataset
- [ ] RAGAS integration
- [ ] Retrieval metrics
- [ ] Hallucination analysis
- [ ] Automated evaluation pipeline

## Phase 4 — AI Engineering

- [ ] FastAPI
- [ ] Unit tests
- [ ] Integration tests
- [ ] Error handling
- [ ] Logging

## Phase 5 — MLOps

- [ ] MLflow
- [ ] Docker
- [ ] CI/CD
- [ ] Model/version tracking

## Phase 6 — Production

- [ ] Cloud deployment
- [ ] Monitoring
- [ ] Performance optimization
- [ ] Cost optimization
- [ ] Load testing

---

# 🔬 Research Questions

This project will investigate several practical questions:

### Retrieval

> Does hybrid retrieval outperform pure vector search?

### Embeddings

> Which embedding model provides the best accuracy/latency trade-off?

### Reranking

> Does reranking significantly improve answer quality?

### Chunking

> How does chunk size affect retrieval and generation quality?

### LLM

> What is the best trade-off between model quality, latency and cost?

### Production

> How can an RAG system maintain stable performance under increasing traffic?

---

# 💼 Business Use Cases

The architecture can be adapted to several enterprise use cases:

- Internal company knowledge assistant
- Legal document analysis
- Financial report analysis
- Technical documentation assistant
- HR knowledge assistant
- Customer support
- Research assistant
- Regulatory document search

---

# 🎓 Skills Demonstrated

This project demonstrates practical skills in:

**Machine Learning**

- Deep Learning
- NLP
- Transformers
- Embeddings
- Information Retrieval

**Generative AI**

- LLMs
- RAG
- Prompt Engineering
- Reranking
- AI Evaluation

**Software Engineering**

- Python
- REST APIs
- Testing
- Git
- Software architecture

**MLOps**

- Docker
- MLflow
- CI/CD
- Monitoring
- Model versioning

**Cloud**

- Deployment
- Infrastructure
- Scalability

---

# 👩‍💻 Author

**Malika Gareh**

AI Engineer | Centrale Lyon

Interested in:

- Artificial Intelligence
- Machine Learning
- Generative AI
- Computer Vision
- MLOps
- AI Engineering

---

# 📌 Project Goal

The final objective is to demonstrate the ability to move from:

```text
AI Model
    ↓
Prototype
    ↓
Evaluated System
    ↓
Production API
    ↓
Monitored AI Application
```

rather than building only a proof-of-concept chatbot.
