# AGNO RAG Chatbot API – Project Documentation

## Overview

This project implements a Retrieval-Augmented Generation (RAG) chatbot API using FastAPI, AGNO, LanceDB, and Sentence Transformers.

The system retrieves relevant information from AGNO documentation and generates grounded responses using OpenRouter GPT-4o-mini.

# Project Goals

\- Build a lightweight RAG chatbot API

\- Retrieve contextual information from documentation

\- Generate accurate AI responses using retrieved content

\- Maintain conversational history for better continuity

\- Expose the system through FastAPI endpoints

# Tech Stack

FastAPI - API framework

AGNO - Agent orchestration

OpenRouter GPT-4o-mini - LLM response generation

LanceDB - Vector database

Sentence Transformers - Embedding generation

Requests - Download documentation

Uvicorn - API server

# Workflow

## 1\. Load Documentation

The application downloads AGNO markdown documentation from predefined URLs.

## 2\. Chunking

Large documents are split into overlapping chunks for efficient semantic retrieval.

## 3\. Embedding Generation

Embeddings are generated using the local model:

\`all-MiniLM-L6-v2\`

## 4\. Store in LanceDB

All chunk vectors and metadata are stored in LanceDB.

## 5\. Retrieval

When a user asks a question:

\- The query is embedded

\- Similar chunks are retrieved

\- Context is prepared for the LLM

## 6\. Response Generation

The AGNO Agent sends the prompt and retrieved context to GPT-4o-mini.

## 7\. Chat History

Recent conversation history is included to improve continuity.

# API Endpoint

## POST /chat

### Request

\`\`\`json

{

"query": "What is AGNO?",

"top\_k": 5

}

\`\`\`

### Response

\`\`\`json

{

"query": "What is AGNO?",

"answer": "Generated response",

"sources": \["source\_url"\],

"response\_time\_seconds": 1.25

}

\`\`\`

# Key Features

\- Retrieval-Augmented Generation (RAG)

\- Semantic search

\- Vector similarity retrieval

\- FastAPI REST API

\- Context-aware responses

\- Conversation memory support

\- Local embedding generation

# Future Enhancements

\- Persistent chat history storage

\- Streaming responses

\- Authentication and security

\- UI integration

\- Additional document sources

\- Hybrid search optimization

# Run Command

uvicorn rag\_chatbot:app –reload

# Conclusion

This project demonstrates a complete RAG-based conversational API using AGNO, FastAPI, vector search, and LLM orchestration in a scalable and modular architecture.