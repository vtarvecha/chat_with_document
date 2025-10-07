RAG-Powered PDF Chat Agent Setup Guide
This guide outlines the steps to create a Retrieval-Augmented Generation (RAG) agent that allows you to chat with the content of your PDF documents.

1. Prerequisites
Python: Ensure you have Python 3.9+ installed.

Google AI API Key: You need a Gemini API Key. Set this key as an environment variable named GOOGLE_API_KEY.

Linux/macOS:

export GOOGLE_API_KEY="YOUR_API_KEY_HERE"

Windows (CMD):

set GOOGLE_API_KEY="YOUR_API_KEY_HERE"

Windows (PowerShell):

$env:GOOGLE_API_KEY="YOUR_API_KEY_HERE"

2. Installation
Open your terminal or command prompt and install the required Python libraries.

pip install streamlit pypdf langchain langchain-google-genai faiss-cpu python-dotenv

Library

Purpose

streamlit

Creates the interactive web UI (frontend).

pypdf

Reads and extracts text from the uploaded PDF document.

langchain

The RAG framework, managing the full workflow.

langchain-google-genai

Integration package for using Gemini models for chat and embeddings.

faiss-cpu

The in-memory vector database for fast similarity search.

python-dotenv

(Optional, but recommended) Helps load environment variables easily.

3. The RAG Architecture Overview
The Python script implements the following steps:

Loading: The user uploads a PDF, and pypdf extracts all the text.

Chunking: The text is split into small, manageable chunks (e.g., 1000 characters each) to fit the LLM's context window and ensure high retrieval relevance.

Embedding: The Gemini Embedding Model (text-embedding-004) converts each text chunk into a dense numerical vector.

Indexing: The vectors are stored in the FAISS Vector Store for efficient similarity search.

Retrieval: When the user asks a question, the question is also converted into a vector. FAISS finds the most similar vectors (and their corresponding text chunks) from the PDF.

Generation: The retrieved chunks (context) and the user's original question are sent to the Gemini Chat Model (gemini-2.5-flash) via a LangChain Conversational Retrieval Chain. The LLM uses the provided context to generate a grounded, accurate answer.
