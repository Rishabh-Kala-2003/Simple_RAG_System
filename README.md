# Simple RAG System

A Retrieval-Augmented Generation (RAG) pipeline that lets you chat with your PDF documents using natural language.

## What it does

Drop PDF files into a folder, run the script, and ask questions about them in plain English. The system retrieves the most relevant sections from your documents and generates accurate, context-aware answers.

## How it works

```
PDF Documents → Text Extraction → Chunking → Embeddings → Vector Store → Query → Answer
```

1. **Document Loading** — Reads all PDFs from the `pdf/` directory using LangChain's PyPDFDirectoryLoader
2. **Text Splitting** — Breaks documents into chunks of 500 characters with 20-char overlap using RecursiveCharacterTextSplitter
3. **Embedding Generation** — Converts text chunks into 768-dimensional vectors using Google's Generative AI Embeddings (`embedding-001`)
4. **Vector Storage** — Stores embeddings in a Pinecone serverless index (AWS, cosine similarity) for fast retrieval
5. **Question Answering** — Uses Google Gemini 1.5 Flash as the LLM with LangChain's RetrievalQA chain to generate answers from retrieved context

## Tech stack

- **Python** — Core language
- **LangChain** — Orchestration framework (document loaders, text splitters, QA chains)
- **Google Gemini 1.5 Flash** — LLM for answer generation
- **Google Generative AI Embeddings** — Text-to-vector conversion
- **Pinecone** — Serverless vector database (AWS, us-east-1)

## Setup

### Prerequisites
- Python 3.9+
- Google API key (for Gemini + Embeddings)
- Pinecone API key

### Installation

```bash
pip install langchain langchain-community langchain-google-genai langchain-pinecone pinecone-client pypdf
```

### Configuration

Create a `config.py` file:

```python
GOOGLE_API_KEY = "your-google-api-key"
PINECONE_API_KEY = "your-pinecone-api-key"
```

### Run

1. Place your PDF files in the `pdf/` directory
2. Run the script:

```bash
python main.py
```

3. Start asking questions at the prompt. Type `exit` to quit.

```
Input Prompt: What are the key findings in this document?
Answer: Based on the document...

Input Prompt: exit
Exiting
```

## Project structure

```
Simple_RAG_System/
├── main.py          # Main RAG pipeline
├── config.py        # API keys configuration
└── pdf/             # Drop your PDF files here
```

## License

MIT
