# Agentic RAG System

##  Overview
This project implements an Agentic Retrieval-Augmented Generation (RAG) system that intelligently decides how to answer a query instead of blindly retrieving information.

The system classifies queries into:
- Factual
- Synthesis
- Out-of-Scope

Based on classification, it retrieves relevant data or declines to answer.

---

##  System Architecture

1. **Document Ingestion**
   - Input: 4 AI regulation documents (.txt)
   - Chunking: 300 words with 50-word overlap

2. **Embedding & Indexing**
   - Model: all-MiniLM-L6-v2
   - Vector Store: FAISS

3. **Query Routing (Explicit Logic)**
   - Factual → direct answer
   - Synthesis → multi-chunk retrieval
   - Out-of-Scope → decline response

4. **Answer Generation**
   - Based on retrieved chunks
   - No hallucination allowed

5. **Evaluation Framework**
   - 15 queries (5 per type)
   - Metrics:
     - Routing Accuracy
     - ROUGE Score

---

##  Chunking Strategy

- Chunk Size: 300 words  
- Overlap: 50 words  

**Reason:**  
Balances context retention and retrieval precision.

---

##  Routing Logic

Rule-based classification using keywords:

- Factual → "what", "who", "define"
- Synthesis → "compare", "analyze", "impact"
- Out-of-Scope → default fallback

This ensures transparency and explainability.

---

##  Evaluation

- Total Queries: 15  
- Categories:
  - 5 Factual
  - 5 Synthesis
  - 5 Out-of-Scope

### Metrics:
- **Routing Accuracy**
- **ROUGE-1 Score**

---

## Results Summary

- Routing Accuracy: ~0.8 (depends on run)
- ROUGE Score: Moderate (due to simple answer generation)

---

##  Failure Analysis

### 1. Routing Errors
- Keyword-based classification can misclassify queries.

### 2. Retrieval Issues
- Important information split across chunks.

### 3. Weak Answer Quality
- Answers are concatenated chunks, not synthesized summaries.

### 4. Contradictory Data Handling
- System does not resolve conflicts across documents.



1. Upload documents (.txt)
2. Run notebook cells
3. Execute evaluation
4. Results saved as `results.csv`

---


- No LangChain agents used (as per constraint)
- Fully explainable routing logic
- Out-of-scope queries handled safely (no hallucination)

---
