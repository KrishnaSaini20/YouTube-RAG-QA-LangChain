# YouTube Video Q&A using RAG and LangChain

## Overview

This project implements a Retrieval-Augmented Generation (RAG) pipeline that allows users to ask questions about YouTube videos using their transcripts.

The system extracts video transcripts, splits them into smaller chunks, converts them into vector embeddings, and stores them in a FAISS vector database.

When a user asks a question, the system retrieves the most relevant transcript chunks and passes them to an OpenAI language model to generate a context-aware response.

The project demonstrates how RAG combines information retrieval with Large Language Models (LLMs) to answer questions based on external knowledge.

## Features

- Extract transcripts from YouTube videos.
- Split large transcripts into manageable text chunks.
- Generate semantic embeddings using OpenAI.
- Store and search embeddings using FAISS.
- Retrieve relevant information through similarity search.
- Generate answers using GPT-4o-mini.
- Reduce unsupported responses through context-based prompting.
- Build a modular RAG pipeline using LangChain Expression Language (LCEL).
- Generate video summaries and answer transcript-related questions.

## Technologies Used

| Technology | Purpose |
|---|---|
| Python | Core programming language |
| LangChain | RAG pipeline orchestration |
| OpenAI GPT-4o-mini | Answer generation |
| OpenAI Embeddings | Text vectorization |
| FAISS | Vector storage and similarity search |
| YouTube Transcript API | Transcript extraction |
| Tiktoken | Tokenization utilities |

## RAG Architecture

The system consists of two major stages.

### 1. Indexing Pipeline

YouTube Video → Transcript Extraction → Text Chunking → Embedding Generation → FAISS Vector Store

### 2. Retrieval and Generation Pipeline

User Question → Similarity Search → Relevant Documents → Prompt Augmentation → LLM → Generated Answer

## Implementation Details

### Step 1: Transcript Extraction

The system extracts English transcripts from a YouTube video using the YouTube Transcript API.

### Step 2: Text Chunking

The extracted transcript is divided into smaller sections using RecursiveCharacterTextSplitter.

Configuration:

- Chunk Size: 1000
- Chunk Overlap: 200

### Step 3: Embedding Generation

Text chunks are converted into vector representations using OpenAI's `text-embedding-3-small` model.

### Step 4: Vector Storage

The embeddings are stored in FAISS, enabling efficient similarity-based document retrieval.

### Step 5: Retrieval

The system retrieves the four most relevant transcript chunks for each user question.

### Step 6: Prompt Augmentation

Retrieved chunks are combined with the user's question to create a context-aware prompt.

The prompt instructs the language model to answer using only the provided transcript context.

### Step 7: Answer Generation

The augmented prompt is passed to GPT-4o-mini to generate a natural-language response.

### Step 8: LCEL Chain

The complete pipeline is connected using LangChain Expression Language with:

- RunnableParallel
- RunnablePassthrough
- RunnableLambda
- PromptTemplate
- StrOutputParser

## Project Structure

```text
YouTube-RAG-QA-LangChain/
│
├── rag_using_langchain.ipynb
├── README.md
├── requirements.txt
├── .gitignore
└── .env.example
```

## Installation and Setup

### 1. Clone the Repository

```bash
git clone https://github.com/USERNAME/YouTube-RAG-QA-LangChain.git
cd YouTube-RAG-QA-LangChain
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

### 3. Configure OpenAI API Key

Create a `.env` file:

```env
OPENAI_API_KEY=your_openai_api_key
```

Never commit your actual API key to GitHub.

### 4. Run the Notebook

Open the notebook in Jupyter Notebook or Google Colab.

Ensure the notebook loads the API key from the environment before running the RAG pipeline.

## Example Queries

The project demonstrates questions such as:

- What is DeepMind?
- Is nuclear fusion discussed in this video?
- Who is Demis Hassabis?
- Can you summarize the video?

The model retrieves relevant transcript sections and generates answers using the retrieved context.

## Key Learnings

This project helped me understand:

- Retrieval-Augmented Generation (RAG).
- LangChain framework and LCEL.
- Text embeddings and semantic similarity.
- Vector databases using FAISS.
- Document chunking and retrieval strategies.
- Prompt engineering.
- Integration of LLMs with external knowledge sources.

## Limitations

- Requires videos with accessible transcripts.
- Depends on OpenAI API access.
- Retrieval quality depends on transcript quality.
- Uses a fixed number of retrieved chunks.
- The notebook demonstrates a single-video RAG workflow.
- Generated answers may still contain inaccuracies.

## Future Improvements

- Build a Streamlit or Gradio user interface.
- Support multiple YouTube videos.
- Add timestamps and source references to answers.
- Implement conversation history.
- Experiment with different embedding models.
- Add retrieval evaluation and answer quality metrics.
- Support local open-source LLMs.

## Author

**Your Name**

GitHub: https://github.com/USERNAME

---

*An NLP and Generative AI project demonstrating Retrieval-Augmented Generation using LangChain, OpenAI, and FAISS.*
