# NovaCrest — Salesforce CRM Knowledge Assistant

## Project Overview

NovaCrest is a Retrieval-Augmented Generation (RAG) application designed to answer questions about Salesforce CRM using retrieved information from Salesforce documentation.

The application combines semantic document retrieval, an AI language model, a Flask REST API, and an interactive Streamlit frontend.

Developed as part of hands-on AI and machine learning training.

## Key Features

- AI-assisted question answering for Salesforce documentation
- Semantic document search using FAISS
- Hugging Face embeddings for document retrieval
- GPT-4o-mini for answer generation
- Answers based on retrieved Salesforce documentation
- Option to display relevant document passages alongside answers
- Configurable retrieval and generation parameters
- Separate backend and frontend components
- Docker configuration for application deployment

## Technologies Used

- Python
- Flask
- Streamlit
- LangChain
- FAISS
- Hugging Face Embeddings (`BAAI/bge-base-en-v1.5`)
- OpenAI GPT-4o-mini
- Docker
- Requests

## Application Architecture

1. A user enters a Salesforce question through the Streamlit interface.
2. Streamlit sends a JSON request to the Flask backend.
3. The backend searches the saved FAISS vector store for relevant documentation.
4. Retrieved passages are supplied to GPT-4o-mini with Salesforce-specific response instructions.
5. The backend returns the generated answer.
6. Streamlit displays the answer and, optionally, the retrieved supporting passages.

## API Endpoints

| Endpoint | Description |
|---|---|
| `GET /` | API welcome message |
| `POST /v1/relevant_chunks` | Retrieve relevant Salesforce documentation |
| `POST /v1/answer` | Generate an answer |
| `POST /v1/answer_with_relevant_chunks` | Generate an answer and return supporting passages |

## Streamlit User Interface

The frontend includes:

- A text field for Salesforce questions
- Retrieval count slider (1–10 chunks, default 2)
- Temperature slider (0.0–1.0, default 0.0)
- Maximum-token slider (64–2048, default 512)
- Answer only and Answer + Relevant Chunks response modes
- Expandable sections for reviewing retrieved document passages
- Error handling for unsuccessful API requests and connection failures

## Salesforce Knowledge Support

The application's prompts are designed to preserve important Salesforce documentation details, including:

- Feature names and supported functionality
- Objects and fields
- User roles and permissions
- Configuration requirements
- Setup and troubleshooting procedures
- Prerequisites, limitations, and exceptions

When the available documentation is insufficient or conflicting, the model is instructed to acknowledge the limitation rather than invent an answer.

These instructions are intended to improve reliability but do not guarantee that every generated response will be correct.

## Example Questions

- Can Salesforce be used on mobile devices?
- Which Salesforce editions support Sales Cloud Einstein?
- What configuration requirements apply to a particular Salesforce feature?

Answers depend on the information available in the saved document vector store.

## Repository Structure

```text
novacrest-qna/
├── backend/
│   ├── app.py
│   ├── rag_utils.py
│   ├── requirements.txt
│   ├── Dockerfile
│   └── faiss_index/
├── frontend/
│   ├── app.py
│   ├── requirements.txt
│   └── Dockerfile
└── README.md
```

## Configuration

The backend uses environment variables for language model access:

- `OPENAI_API_KEY`
- `OPENAI_API_BASE`

The frontend is configured to communicate with the backend at `http://localhost:7860`.

The saved FAISS index should only be loaded from a trusted source because the backend enables pickle deserialization.

## Project Purpose

This project demonstrates the integration of semantic search, retrieval-augmented generation, REST API development, and interactive application deployment to support technical knowledge retrieval.

## Author

Victor Marek II

GitHub: https://github.com/VicGL156
