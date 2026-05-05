# 2A202600218_NguyenTienDat_Lab19_track3
---

# 🚀 GraphRAG System – Tech Company Corpus

## 📌 Overview

This project implements a **GraphRAG (Graph-based Retrieval Augmented Generation)** system to improve question answering over a Tech Company dataset.

We compare:

* **Flat RAG** (vector-based retrieval)
* **GraphRAG** (knowledge graph + multi-hop reasoning)

---

## ⚙️ Pipeline

### 1. Entity & Relation Extraction

* Use LLM to extract triples from text
* Example:

```
(OpenAI, FOUNDED_BY, Sam Altman)
(OpenAI, FOUNDED_BY, Elon Musk)
(OpenAI, FOUNDED_IN, 2015)
```

---

### 2. Graph Construction

* Build Knowledge Graph using **NetworkX**
* Nodes: entities (company, person)
* Edges: relations (FOUNDED_BY, ACQUIRED_BY, …)

---

### 3. Querying (GraphRAG)

* Extract entity from question
* Traverse graph using **2-hop BFS**
* Convert subgraph → text → send to LLM

---

### 4. Baseline (Flat RAG)

* Use text retrieval (TF-IDF / vector search)
* No structured reasoning

---

## 📊 Results (20 Questions Benchmark)

| Method   | Accuracy |
| -------- | -------- |
| Flat RAG | 55%      |
| GraphRAG | 100%     |

👉 GraphRAG significantly outperforms Flat RAG, especially in **multi-hop reasoning tasks**.

---

## 🧠 Key Insights

### ❌ Flat RAG limitations

* Cannot handle multi-hop reasoning
* Easily retrieves irrelevant context
* Higher hallucination risk

### ✅ GraphRAG advantages

* Uses structured knowledge graph
* Supports multi-step reasoning
* More accurate and consistent answers

---

## 💰 Cost Analysis

* **Flat RAG**: faster, lower token usage
* **GraphRAG**: higher cost (graph building + traversal)
* Trade-off:
  → GraphRAG = higher cost but much better accuracy

---

## 📁 Deliverables

* ✅ Source code (.ipynb)
* ✅ Knowledge graph visualization
* ✅ Benchmark results (20 questions)
* ✅ Accuracy comparison & analysis

---

## 🏁 Conclusion

GraphRAG provides a more reliable and powerful approach for QA systems by leveraging structured knowledge and multi-hop reasoning, making it superior to traditional Flat RAG in complex queries.

---

