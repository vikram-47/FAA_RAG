📚 Aerospace RAG System – FAA Document Question Answering
🚀 Overview

This project implements a Retrieval-Augmented Generation (RAG) system designed to answer technical questions from FAA aerospace regulatory documents.

Instead of relying purely on a language model’s internal knowledge, this system retrieves relevant context from official FAA PDFs and uses a Large Language Model (LLM) to generate grounded answers.

The system reduces hallucination by enforcing context-based answering.

🧠 Problem Statement

Large Language Models tend to:

Hallucinate answers

Provide incorrect domain-specific information

Answer questions outside their training knowledge

This project solves that by:

Embedding FAA documents into a vector database

Retrieving semantically relevant chunks

Passing only retrieved context to the LLM

Enforcing strict answer constraints

If the answer is not found in the retrieved context, the system responds with:

"I could not find this information in the provided documents."

🏗️ Architecture

User Question
⬇
FAISS Vector Store (Semantic Search)
⬇
Top-k Relevant Document Chunks
⬇
Prompt Template (Context + Question)
⬇
Mistral-7B-Instruct LLM
⬇
Final Answer

🔧 Tech Stack

LangChain

FAISS (Vector Store)

HuggingFace Transformers

Mistral-7B-Instruct

SentenceTransformers (all-MiniLM-L6-v2) for embeddings

PyPDF for document loading

Google Colab (T4 GPU, 4-bit quantization)

📂 Documents Used

The system indexes multiple FAA Advisory Circulars, including:

Damage Tolerance and Fatigue Evaluation

Metallic Structures Evaluation

Composite Structures

Inspection & Maintenance Guidelines

Alterations and Repairs

Thermal Fatigue Documentation

Each document is categorized and chunked before embedding.

🔍 Key Features

Semantic search using dense embeddings

FAISS similarity retrieval

4-bit quantized LLM for efficient GPU usage

Context-restricted answering

Hallucination control via strict prompting

Category-based filtering support

Adjustable similarity score threshold

⚙️ Retrieval Strategy

Chunk size optimized for technical PDF structure

Top-k retrieval

Optional similarity score threshold filtering

Metadata-based filtering (e.g., category: Inspection, Structures, Damage)

🛑 Hallucination Control

The system enforces a strict instruction:

If the answer is not in the context, respond with:
"I could not find this information in the provided documents."

This ensures:

No external knowledge leakage

Domain-grounded answers

Reliable regulatory responses

🧪 Example Query

Question:
What are acceptable methods for aircraft crack inspection?

Answer (Generated from FAA documents):
Visual inspection, ultrasonic inspection, radiography, and eddy current inspection.

