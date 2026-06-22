# LangChain, Embeddings & ChromaDB Basics

## Overview

This project demonstrates the fundamental concepts behind Retrieval-Augmented Generation (RAG) systems using:

* LangChain
* Sentence Transformers
* Embeddings
* Vector Databases
* ChromaDB

The application loads text documents, converts them into vector embeddings, stores them in ChromaDB, and retrieves the most relevant documents based on a user query.

---

## What You Will Learn

### 1. LangChain

LangChain is a framework used to build applications powered by Large Language Models (LLMs).

Key Features:

* Document Loading
* Text Splitting
* Embedding Generation
* Vector Database Integration
* Retrieval-Augmented Generation (RAG)
* Agent Development

---

### 2. Embeddings

Embeddings are numerical vector representations of text.

Example:

Text:

```text
Python is a programming language.
```

Embedding:

```text
[0.12, -0.45, 0.67, ...]
```

Benefits:

* Capture semantic meaning
* Enable similarity search
* Support document retrieval

In this project, embeddings are generated using:

```python
SentenceTransformer("all-MiniLM-L6-v2")
```

Embedding Dimension:

```text
384
```

---

### 3. Vector Database

A Vector Database stores embeddings and performs similarity searches.

Unlike traditional databases:

| Traditional DB | Vector DB         |
| -------------- | ----------------- |
| Exact Match    | Semantic Match    |
| SQL Queries    | Similarity Search |
| Text Storage   | Vector Storage    |

Popular Vector Databases:

* ChromaDB
* Pinecone
* Weaviate
* FAISS
* Milvus

---

### 4. ChromaDB

ChromaDB is an open-source vector database designed for AI applications.

Features:

* Lightweight
* Easy to use
* Local storage support
* Fast similarity search
* LangChain integration

Creating a collection:

```python
collection = client.get_or_create_collection(
    name="text_collection"
)
```

---

## Project Workflow

### Step 1: Load Documents

Load text files using LangChain.

```python
loader = DirectoryLoader(
    "../data/text_files",
    glob="*.txt",
    loader_cls=TextLoader
)

documents = loader.load()
```

---

### Step 2: Extract Text

```python
texts = [doc.page_content for doc in documents]
```

---

### Step 3: Generate Embeddings

```python
model = SentenceTransformer("all-MiniLM-L6-v2")

embeddings = model.encode(texts)
```

Output:

```text
(2, 384)
```

Meaning:

* 2 documents
* 384-dimensional embeddings

---

### Step 4: Store Embeddings in ChromaDB

```python
collection.add(
    ids=ids,
    documents=texts,
    embeddings=embeddings.tolist()
)
```

---

### Step 5: Query the Database

```python
query_embedding = model.encode([query])

results = collection.query(
    query_embeddings=query_embedding.tolist(),
    n_results=2
)
```

---

### Step 6: Retrieve Relevant Documents

The system returns the most semantically similar documents.

Example:

Query:

```text
What is Python?
```

Result:

```text
Python Programming Introduction
Python is a high-level programming language...
```

---

## Project Structure

```text
project/
│
├── data/
│   └── text_files/
│       ├── file1.txt
│       └── file2.txt
│
├── notebook/
│   └── document.ipynb
│
├── requirements.txt
│
└── README.md
```

---

## Installation

Clone the repository:

```bash
git clone <repository-url>
```

Create Virtual Environment:

```bash
python -m venv venv
```

Activate Environment:

### Windows

```bash
venv\Scripts\activate
```

### Linux / Mac

```bash
source venv/bin/activate
```

Install Dependencies:

```bash
pip install -r requirements.txt
```

---

## Required Libraries

```bash
pip install langchain-community
pip install sentence-transformers
pip install chromadb
pip install pypdf
pip install ipywidgets
```

---

## Applications

* Semantic Search
* Question Answering Systems
* Chatbots
* Knowledge Bases
* Document Retrieval
* RAG Applications

---

## Future Enhancements

* PDF Support
* Chunking Large Documents
* LangChain Retrievers
* OpenAI Integration
* Conversational RAG
* Memory-Based Chatbots

---

## Key Concepts Summary

| Concept         | Description                             |
| --------------- | --------------------------------------- |
| LangChain       | Framework for LLM Applications          |
| Embeddings      | Numerical representation of text        |
| Vector Database | Stores embeddings for similarity search |
| ChromaDB        | Open-source vector database             |
| Retrieval       | Finding relevant documents              |
| RAG             | Retrieval-Augmented Generation          |

---

## Conclusion

This project provides a beginner-friendly introduction to LangChain, Embeddings, Vector Databases, and ChromaDB. It demonstrates how textual data can be transformed into embeddings, stored efficiently in a vector database, and retrieved using semantic similarity search, forming the foundation of modern RAG-based AI systems.
