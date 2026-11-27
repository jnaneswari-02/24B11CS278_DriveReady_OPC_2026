# Day 5 – PDF-Based Retrieval-Augmented Generation (RAG)

## Project Overview
This project implements a PDF-based Retrieval-Augmented Generation (RAG) system using Python, Sentence Transformers, FAISS, and the Groq API.

The system extracts text from an uploaded PDF, divides it into smaller chunks, converts the chunks into vector embeddings, and stores them in a FAISS index. When a user asks a question, the system retrieves the most relevant PDF content and uses the Groq language model to generate an answer based on that context.

## Objectives
- Understand the concept of Retrieval-Augmented Generation (RAG).
- Extract text from PDF documents.
- Handle scanned PDFs using OCR.
- Split large documents into smaller text chunks.
- Generate embeddings using Sentence Transformers.
- Store and search embeddings using FAISS.
- Retrieve relevant information based on user questions.
- Generate context-based answers using the Groq API.

## Technologies Used
- **Python** – Main programming language.
- **Google Colab** – Development environment.
- **PyMuPDF** – Extracting text from PDF files.
- **Pytesseract and EasyOCR** – OCR support for scanned documents.
- **Sentence Transformers** – Generating text embeddings.
- **FAISS** – Efficient similarity search and retrieval.
- **Groq API** – Generating answers using a language model.
- **NumPy** – Numerical operations on embeddings.

## Project Workflow

1. **Embedding Model Comparison:** Load and compare Sentence Transformer models such as `all-MiniLM-L6-v2` and `all-mpnet-base-v2`.
2. **PDF Upload:** Upload a PDF document through Google Colab.
3. **Text Extraction:** Extract text from the PDF using PyMuPDF. OCR is used for scanned or image-based pages where text extraction is unavailable.
4. **Text Chunking:** Divide the extracted text into smaller chunks of 500 characters with an overlap of 100 characters.
5. **Embedding Generation:** Convert the text chunks into numerical vector embeddings using `all-MiniLM-L6-v2`.
6. **FAISS Indexing:** Store normalized embeddings in a FAISS `IndexFlatIP` index for similarity-based retrieval.
7. **Information Retrieval:** Retrieve the top 3 relevant chunks based on the user's question.
8. **Answer Generation:** Send the retrieved context and question to the Groq language model to generate an answer grounded in the PDF.
9. **Interactive Question Answering:** Allow users to ask multiple questions about the uploaded PDF until they type `exit`.

## Installation and Setup

The notebook is designed to run in Google Colab.

### Step 1: Open the Notebook
Open `RAG-2.ipynb` in Google Colab.

### Step 2: Install Dependencies
Run the installation cells in the notebook to install the required Python libraries and OCR dependencies.

### Step 3: Upload a PDF
Upload the PDF document when prompted by the notebook.

### Step 4: Configure Groq API Key
Provide a valid Groq API key when prompted. Keep the API key private and do not upload it to GitHub.

### Step 5: Run All Cells
Execute the notebook cells in the correct order to extract the PDF content, generate embeddings, build the FAISS index, and start the question-answering system.

## Example Usage

After uploading a PDF, the system allows users to ask questions related to its content.

Example:

- **User:** What is the main topic of this document?
- **System:** Retrieves relevant text from the PDF and generates an answer using the retrieved context.

Type `exit` to stop the interactive question-answering loop.

## Key Learnings
- Understanding the architecture of a RAG system.
- Working with PDF text extraction and OCR.
- Understanding text chunking and overlapping.
- Generating vector embeddings using Sentence Transformers.
- Performing similarity search using FAISS.
- Connecting a retrieval system with a Large Language Model.
- Building a document-based question-answering application.

## Conclusion
This project demonstrates how Retrieval-Augmented Generation can be used to build a document-based question-answering system. By combining PDF extraction, OCR, embeddings, FAISS retrieval, and the Groq API, users can ask questions and receive answers based on the content of their uploaded PDF documents.
