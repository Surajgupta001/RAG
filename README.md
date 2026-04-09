# 🚀 Retrieval-Augmented Generation (RAG) Masterclass

Welcome to the **Retrieval-Augmented Generation (RAG)** project! This repository serves as a comprehensive guide and implementation of RAG pipelines, ranging from basic document retrieval to advanced **Agentic RAG workflows**.

## 1. Introduction: What is RAG?

**Retrieval-Augmented Generation (RAG)** is an AI framework that connects Large Language Models (LLMs) to external knowledge bases.

Think of an LLM like a highly intelligent student taking an open-book exam. By default, the student (LLM) only knows what they memorized before the test (its training data). RAG gives the student access to a library of specific, up-to-date textbooks (your documents) to look up answers before writing them down.

### How it Works:
1. **Retrieval:** When a user asks a question, the system searches a specialized database (Vector Store) for the most relevant information.
2. **Generation:** The retrieved information is provided to the LLM as context, and the LLM generates a precise, well-informed answer.

## 2. Why RAG? & Use Cases

### Why not just use traditional LLMs?
* **Eliminates Hallucinations:** Prevents the LLM from making up facts because it bases answers on your specific documents.
* **Up-to-date Knowledge:** You can add new documents anytime without needing to expensively retrain the LLM.
* **Data Privacy:** Your private data stays in your secure database instead of being sent to public models for training.
* **Source Tracking:** RAG can cite the exact document and page number it used to generate the answer.

### Real-World Use Cases
* 💬 **Customer Support Chatbots:** Instantly answering queries using company knowledge bases.
* 📄 **Document Q&A:** Chatting with massive PDFs, legal contracts, or financial reports.
* 🧠 **Internal Knowledge Assistants:** Helping employees find HR policies or engineering documentation fast.

## 3. Project Overview

This project provides a hands-on implementation of various RAG architectures. It starts with a foundational document-based RAG pipeline and advances into an intelligent **Agentic RAG** system that can independently decide when to search for data and when to answer directly.

### High-Level Workflow
The core workflow involves loading documents (PDFs, text files), slicing them into manageable chunks, converting those chunks into numerical embeddings, and storing them in an efficient vector database. Once queried, the system retrieves the most similar chunks and seamlessly passes them to an LLM to generate a natural response.

## 4. Tech Stack

This project leverages modern AI frameworks and powerful models:

* **Programming Language:** Python 🐍
* **Frameworks:** LangChain, LangGraph
* **Large Language Models (LLMs):** Groq (`llama-3.1-8b-instant`), Google Generative AI
* **Embeddings:** Google Gemini Embeddings, Sentence Transformers
* **Vector Databases:** FAISS, ChromaDB, Typesense
* **Document Processing:** PyMuPDF, Unstructured, LangChain Text Splitters

## 5. Codebase Explanation

Here is a breakdown of the project directory structure to help you get started:

* 📁 **`data/`** - The storage hub for your raw files and databases.
  * `pdfs/` - Drop your PDF documents here for processing.
  * `text_files/` - Store your raw text documents here.
  * `vector_store/` - The generated local vector databases (like FAISS indices) are saved here.
* 📁 **`notebook/`** - Educational playground.
  * `document.ipynb` - A step-by-step Jupyter Notebook detailing the standard RAG pipeline (Loading, Chunking, Embedding, Retrieving).
* 📁 **`agenticRag/`** - Advanced implementations.
  * `1-agenticRag.ipynb` - Implements an intelligent, state-based workflow using **LangGraph**. The agent actively decides if retrieval is necessary before generating a response.
* 📄 **`typesense.ipynb`** - Implementation of RAG utilizing Typesense as the high-performance search engine/vector store.
* 📄 **`requirements.txt`** - Defines all the Python dependencies required to run the project.

## 6. Pipeline Explanation

At its core, a RAG pipeline operates through a sequence of data transformations:

1. **📥 Data Loading:** Extracting raw text from various sources like PDFs (`pdfs/`), JSONL (`books.jsonl`), or text files.
2. **✂️ Chunking:** Splitting large documents into smaller, meaningful segments (chunks). This ensures we only search for specific contexts, reducing noise.
3. **🔢 Embedding:** Converting the text chunks into mathematical vectors (lists of numbers) using embedding models (e.g., Gemini's embedding model).
4. **💾 Storage:** Saving these vectors into a Vector Database (FAISS, Chroma, or Typesense) for lightning-fast similarity search.
5. **🔍 Retrieval:** When a user asks a question, the query is embedded, and the database returns the most mathematically similar text chunks.
6. **✨ Generation:** The retrieved chunks are injected into the prompt of the LLM (like Groq's LLaMA 3.1) to synthesize the final, accurate response.

## 7. How to Run

Follow these steps to set up the project on your local machine:

### Prerequisites
* Python 3.9+
* API Keys for Groq and Google Gemini

### Setup Instructions
1. **Clone the repository:**
   ```bash
   git clone <your-repo-url>
   cd RAG
   ```

2. **Create a Virtual Environment (Optional but recommended):**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows use: venv\Scripts\activate
   ```

3. **Install Dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Environment Variables:**
   Create a `.env` file in the root directory and add your API keys:
   ```env
   GROQ_API_KEY=your_groq_key_here
   GOOGLE_API_KEY=your_gemini_key_here
   ```

5. **Run the Notebooks:**
   Launch Jupyter Notebook or Jupyter Lab to explore the pipelines.
   ```bash
   jupyter notebook
   ```
   * Start with `notebook/document.ipynb` to understand the basics.
   * Then explore `agenticRag/1-agenticRag.ipynb` for the advanced graph-based workflow.

## 8. Architecture Overview

### Standard RAG Pipeline
```text
  User Query
      │
      ▼
 ┌─────────┐      🔍 Similarity Search       ┌──────────────┐
 │ Embeddings│ ───────────────────────────► │ Vector Database│ (FAISS/Chroma)
 └─────────┘                                └──────┬───────┘
                                                   │
                                                   ▼
                                            ┌──────────────┐
                                            │ Retrieved    │
                                            │ Context      │
                                            └──────┬───────┘
                                                   │
      ┌────────────────────────────────────────────┘
      │
      ▼
 ┌─────────┐
 │   LLM   │ ───►  Final Output
 └─────────┘
```

### Agentic RAG Workflow (LangGraph)
```text
User Query
    ↓
[ Decide Node ]
    ↓
 ┌───────────────┐
 │ Retrieval?    │
 └──────┬────────┘
        ↓ (Yes)
   [ Retrieve ]
        ↓
   [ Generate ]
        ↓
      END
```

## 9. Features

* 📚 **Multi-format Document Ingestion:** Process PDFs, text files, and structured JSON files.
* 🚀 **High-Speed Inference:** Utilizing Groq for ultra-low latency LLM generation.
* 🧠 **Agentic Decision Making:** The system is smart enough to bypass retrieval if the query doesn't require external context, saving time and tokens.
* 🔧 **Modular Architecture:** Easily swap out different models, embeddings, or vector databases (FAISS, Chroma, Typesense).

## 10. Future Improvements

* [ ] **UI Integration:** Build a friendly front-end interface using Streamlit or Gradio.
* [ ] **Advanced Chunking Strategies:** Implement semantic chunking for better context preservation.
* [ ] **Hybrid Search:** Combine Keyword search (BM25) with Vector search for more resilient multi-modal retrieval.
* [ ] **Memory:** Add conversation history so the agent can handle follow-up questions contextually.
* [ ] **Evaluation:** Integrate tools like RAGAS to programmatically evaluate the accuracy and relevance of the answers.

---
*Built to demonstrate the power of Agentic AI and Retrieval-Augmented Generation.*
