# RAG Sree Sai Ram

A Streamlit-based PDF question-answering application that uses Retrieval-Augmented Generation (RAG). The app lets users upload PDF files, creates a local FAISS vector index from the PDF text, and answers questions using retrieved context with Google Gemini.

## Features

- Upload one or more PDF files from the Streamlit sidebar.
- Extract text from PDFs using `pypdf`.
- Split extracted text into overlapping chunks.
- Generate local embeddings with Hugging Face `sentence-transformers/all-MiniLM-L6-v2`.
- Store and load document vectors using FAISS.
- Answer user questions with Google Gemini through LangChain.
- Return answers only from the uploaded PDF context.

## Project Structure

```text
.
+-- app1.py                    # Main Streamlit RAG application
+-- requirements.txt           # Python dependencies
+-- faiss_index/               # Generated FAISS vector index
+-- attention.pdf              # Sample PDF
+-- attention1.pdf             # Sample PDF
+-- experiment.ipynb           # Experiment notebook
+-- rag_groq_llama33.ipynb     # RAG experiment notebook
+-- .env                       # Local environment variables
```

## Requirements

- Python 3.10 or newer
- Google API key for Gemini
- Internet connection during first run to download the Hugging Face embedding model

## Setup

1. Create and activate a virtual environment:

```powershell
python -m venv venv
.\venv\Scripts\activate
```

2. Install dependencies:

```powershell
pip install -r requirements.txt
```

3. Create a `.env` file in the project root:

```env
GOOGLE_API_KEY=your_google_api_key_here
```

## Run the App

Start the Streamlit application:

```powershell
streamlit run app1.py
```

Then open the local Streamlit URL shown in the terminal, usually:

```text
http://localhost:8501
```

## How to Use

1. Open the Streamlit app in your browser.
2. Upload one or more PDF files from the sidebar.
3. Click `Process PDFs`.
4. Ask a question in the main input box.
5. The app retrieves relevant PDF chunks from FAISS and sends them to Gemini for an answer.

## Notes

- The FAISS index is saved in the `faiss_index/` folder.
- If `faiss_index/` already exists, the current app does not rebuild it automatically.
- To index a new set of PDFs from scratch, delete the existing `faiss_index/` folder and process PDFs again.
- Keep `.env` private because it contains your API key.

## Main Technologies

- Streamlit
- LangChain
- Google Gemini
- Hugging Face embeddings
- FAISS
- pypdf

## Troubleshooting

If you see `GOOGLE_API_KEY not found in .env file`, confirm that:

- `.env` exists in the project root.
- It contains `GOOGLE_API_KEY=...`.
- The app is being run from this project folder.

If answers do not reflect newly uploaded PDFs, remove the existing `faiss_index/` folder and process the PDFs again.
