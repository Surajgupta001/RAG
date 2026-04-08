# 🤖 Agentic RAG System using LangGraph + Groq + Gemini

## 📌 Overview

This project implements an **Agentic Retrieval-Augmented Generation (RAG)** system using a **state-based workflow** powered by LangGraph.
The system intelligently decides whether to retrieve information from a vector database or directly generate an answer.

---

## 🚀 Tech Stack

* **Framework:** LangChain + LangGraph
* **LLM:** Groq (`llama-3.1-8b-instant`)
* **Embeddings:** Google Gemini (`gemini-embedding-001` / updated to `text-embedding-004`)
* **Vector Store:** FAISS
* **Language:** Python

---

## 🧠 Architecture

This project follows an **Agentic RAG pipeline**:

1. **Decision Node**

   * Determines whether retrieval is needed based on the query.

2. **Retrieval Node**

   * Fetches relevant documents from FAISS using embeddings.

3. **Generation Node**

   * Generates the final response using:

     * Retrieved context (RAG mode) OR
     * Direct LLM response (no retrieval)

---

## 🔄 Workflow (LangGraph)

```
User Query
    ↓
[ Decide Node ]
    ↓
 ┌───────────────┐
 │ Retrieval?    │
 └──────┬────────┘
        ↓
   [ Retrieve ]
        ↓
   [ Generate ]
        ↓
      END
```

---

## 📂 Data Handling

* Sample documents are created manually
* Converted into `Document` objects
* Stored in **FAISS vector database**
* Retrieved using semantic similarity search

---

## ⚙️ Key Components

### 1. State Definition

```python
class AgentState(TypedDict):
    question: str
    documents: List[Document]
    answer: str
    need_retrieval: bool
```

---

### 2. Retrieval Decision Logic

* Uses simple keyword-based heuristic:

```python
["what", "how", "explain", "describe", "tell me"]
```

---

### 3. RAG Generation Logic

* If documents exist:

  * Uses **context-aware prompting**
* Else:

  * Direct LLM response

---

## 🧪 Example Queries

* What is LangGraph?
* What are vector databases?
* Explain RAG

---

## 🔥 Key Features

* ✅ Agentic decision-making (not always RAG)
* ✅ Conditional workflow using LangGraph
* ✅ Hybrid response system (RAG + Direct LLM)
* ✅ Fast inference using Groq
* ✅ Semantic retrieval using FAISS

---

## ⚠️ Improvements (Future Work)

* Replace keyword heuristic with LLM-based decision
* Add real-world document ingestion (PDF, web)
* Implement memory (chat history)
* Add streaming responses
* Build UI (Streamlit / React)

---

## 🧠 Learning Outcome

This project demonstrates:

* How **Agentic RAG** works
* How to integrate **LLM + Vector DB**
* How to build **state-based AI workflows**
* Practical usage of **LangGraph**

---

## ✅ Conclusion

This is a **basic but powerful Agentic RAG system** that combines:

* Decision-making
* Retrieval
* Generation

It serves as a strong foundation for building **advanced AI assistants like Jarvis** 🚀
