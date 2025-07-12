# 📚 Academic RAG System

A RAG (Retrieval-Augmented Generation) system that processes university course PDFs and enables intelligent question-answering using local LLMs. Built with **LangChain**, **ChromaDB**, and **Ollama** for private, offline academic document search and retrieval.

---

## Features

* **PDF Document Processing**: Automatically loads and processes PDF files from course materials.
* **Intelligent Chunking**: Splits documents into manageable chunks with overlap for better context preservation.
* **Vector Storage**: Uses ChromaDB for efficient similarity search and document retrieval.
* **Local LLM Integration**: Powered by Ollama with the Mistral model for privacy-focused inference.
* **Source Attribution**: Tracks and displays source documents for each answer.
* **Incremental Updates**: Only processes new documents, avoiding duplicates.

---

## Technology Stack

* **LangChain**: Document processing and RAG pipeline.
* **ChromaDB**: Vector database for embeddings storage.
* **Ollama**: Local LLM inference engine.
* **Mistral**: Embedding and language model.
* **PyPDF**: PDF document loading.

---

## Prerequisites

* Python 3.8+
* Ollama installed and running
* Mistral model pulled in Ollama (`ollama pull mistral`)

---

## Installation

1.  **Clone the repository**:

    ```bash
    git clone [https://github.com/yourusername/academic-rag-system.git](https://github.com/yourusername/academic-rag-system.git)
    cd academic-rag-system
    ```

2.  **Install dependencies**:

    ```bash
    pip install -r requirements.txt
    ```

3.  **Install Ollama and pull Mistral model**:

    ```bash
    # Install Ollama from [https://ollama.ai/](https://ollama.ai/)
    ollama pull mistral
    ```

---

## 📖 Usage

### 1. Add Your PDF Documents

Place your course PDFs in the `data/` directory or update the `DATA_PATH` variable in `main.py`.

### 2. Build the Knowledge Base

```python
# First run - builds the database
main(reset=True)

# Subsequent runs - adds new documents only
main(reset=False)

# Ask questions about your course materials
query_rag("What is machine learning?")
query_rag("Explain the concept of neural networks")
query_rag("What are the main algorithms covered in this course?")

response = query_rag("What is Ant colony optimization")

Output:

Response: Ant Colony Optimization (ACO) is a metaheuristic algorithm inspired by the foraging behavior of ants...
Sources: ['course_material.pdf:15:2', 'algorithms.pdf:8:1']
```

## ⚙️ Configuration

### Key Parameters

* `CHROMA_PATH`: Directory for ChromaDB storage (default: `"chroma_test"`)
* `DATA_PATH`: Directory containing PDF files (default: `"."`)
* `chunk_size`: Text chunk size for processing (default: `800`)
* `chunk_overlap`: Overlap between chunks (default: `80`)
* `k`: Number of similar documents to retrieve (default: `5`)

### Customizing the Model

To use a different Ollama model:

```python
def get_embedding_function():
    embeddings = OllamaEmbeddings(model='llama2')  # Change model here
    return embeddings

# Also update the query model
model = Ollama(model="llama2")
