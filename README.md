# Medical RAG AI Assistant

A Retrieval-Augmented Generation (RAG) based medical AI assistant that uses a large medical reference manual to retrieve relevant information and generate concise, structured responses to healthcare-related questions.

## Overview

Healthcare professionals must often navigate large volumes of medical information when researching symptoms, treatments, diagnoses, and clinical protocols. This project demonstrates how RAG can combine semantic search with a Large Language Model (LLM) to make medical information easier to retrieve and understand.

The system processes a **4,114-page medical reference manual** into searchable document chunks, converts the content into semantic embeddings, stores the embeddings in a vector database, and uses a locally hosted **Mistral 7B** model to generate responses.

## Tech Stack

* **Python**
* **LangChain**
* **ChromaDB**
* **Sentence Transformers**
* **Mistral 7B**
* **Llama.cpp**
* **PyMuPDF**
* **Hugging Face**
* **tiktoken**
* **Pandas**
* **Google Colab**

## RAG Pipeline

```text
Medical PDF
    ↓
PyMuPDF Document Loader
    ↓
Text Chunking
    ↓
Sentence Transformer Embeddings
    ↓
ChromaDB Vector Store
    ↓
Relevant Context Retrieval
    ↓
Mistral 7B LLM
    ↓
Structured Medical Response
```

## Data Processing

The medical reference manual contains over 4,000 pages across multiple medical sections. The project uses `RecursiveCharacterTextSplitter` with a **500-token chunk size** and **50-token overlap**, producing **8,853 searchable document chunks**.
Semantic embeddings are generated using:

```text
sentence-transformers/all-MiniLM-L6-v2
```

Each embedding contains **384 dimensions**.

## LLM

The project uses the quantized:

```text
Mistral 7B Instruct v0.2
```

model through `llama-cpp-python`, allowing the LLM to run locally.

## Prompt Engineering

Prompt engineering was used to encourage the model to produce consistent, structured responses. The generated responses follow three primary sections:

1. **Definition**
2. **Symptoms**
3. **Treatment / Management**

The prompt also instructs the model to provide factual, concise responses and acknowledge uncertainty when appropriate.

## Example Queries

The system was tested on questions involving:

* Critical-care protocols such as sepsis management
* Symptoms and treatment of appendicitis
* Causes and treatment of patchy hair loss
* Traumatic brain injuries
* Emergency care for fractures

## Evaluation

The RAG system was evaluated using **groundedness and relevance**. Example evaluations received scores of **5**, indicating that the generated responses were considered well-supported by the retrieved context and relevant to the questions.

## Key Features

* Processes a large medical knowledge base
* Splits documents into searchable semantic chunks
* Generates 384-dimensional embeddings
* Performs vector-based retrieval with ChromaDB
* Runs Mistral 7B locally using Llama.cpp
* Uses prompt engineering for consistent response formatting
* Evaluates responses based on groundedness and relevance

## Future Improvements

* Continuously update the knowledge base with current medical guidelines and research
* Add confidence thresholds for high-risk queries
* Introduce human review for sensitive medical questions
* Collect user feedback to improve retrieval and response quality
* Expand the medical knowledge base

## Disclaimer

This project is an **AI/educational prototype** and should not be used as a substitute for professional medical advice, diagnosis, or clinical decision-making.
