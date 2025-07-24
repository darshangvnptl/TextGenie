# TextGenie: Intelligent Document Assistant

## Core Idea

**TextGenie** is designed as an intelligent assistant that can answer questions and summarize information from your personal or work-related document collections. Unlike traditional search, this system leverages a Large Language Model (LLM) to synthesize comprehensive answers based on context retrieved directly from your documents.

## Key Features & Scope for this Base Project

### 1. Document Ingestion
* **Format Support:** Initially supports common document formats including `.pdf` and `.txt` files.
* **Storage:** Raw, unprocessed documents are stored securely in the `data/raw` folder.
* **Processing Module:** Includes a dedicated script/module responsible for efficiently loading and preparing these diverse document types.

### 2. Text Chunking & Embedding
* **Chunking Strategy:** Employs a robust text chunking strategy, such as a recursive character text splitter, to break down large documents into manageable, overlapping segments.
* **Embedding Generation:** Generates high-quality vector embeddings for each text chunk using a pre-trained sentence transformer model (e.g., `all-MiniLM-L6-v2` from Hugging Face).
* **Storage:** Processed chunks and their corresponding embeddings are saved in the `data/processed` directory.

### 3. Vector Store Integration
* **Local Storage:** Utilizes a lightweight, local vector store for simplicity, such as FAISS (from `langchain`) or an embedded ChromaDB instance. This eliminates the need for external database setup for initial development.
* **Functionality:** Implements core functions to seamlessly add new documents to the vector store and to perform efficient similarity searches.

### 4. Retrieval Module
* **Relevant Context Retrieval:** Given a user query, this module intelligently retrieves the top `k` most relevant text chunks from the vector store.
* **Query Pre-processing:** Incorporates basic query pre-processing steps, such as text cleaning and lowercasing, to enhance retrieval accuracy.

### 5. Generation Module
* **LLM Integration:** Integrates with a small, open-source Large Language Model (LLM) like Llama 2 7B (quantized), Mistral-7B-v0.1, or similar models available via `ollama` or `transformers`. For quicker setup, an OpenAI or Anthropic API could be used initially if access is available.
* **Prompt Construction:** Constructs a clear and effective prompt that meticulously includes both the user's question and the retrieved contextual information.
* **Answer Synthesis:** Generates a concise and coherent answer or summary, strictly based on the provided context, preventing hallucination.

### 6. User Interface (Basic)
* **Interactive Interface:** Provides a simple command-line interface (CLI) or a basic Streamlit web application for user interaction.
* **Key Interactions:**
    * Allows users to specify a directory for document ingestion.
    * Accepts user questions for querying the documents.
    * Displays the AI-generated answer prominently.
    * (Optional) Provides visibility into the source chunks that were used to formulate the answer, enhancing transparency.