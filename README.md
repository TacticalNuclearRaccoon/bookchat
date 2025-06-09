# Bookchat (ask questions to a book to retrieve information)

BookChat is an interactive command-line tool that allows you to ask questions about the content of a PDF book. It leverages document processing, text chunking, semantic embeddings, and a local language model to provide accurate answers based on the book's content.

** the book needs to be a pdf file **

---

## Features

- **PDF to Markdown Conversion:** Uses Docling to process and convert PDF books into markdown, including OCR and table structure extraction.
- **Semantic Search:** Splits the book into manageable chunks and creates semantic embeddings for efficient retrieval.
- **Local Language Model:** Connects to a local Ollama LLM (default: `mistral:latest`) for fast, private question answering.
- **Persistent Vector Store:** Saves and loads vector indices for fast startup on subsequent runs.
- **Interactive CLI:** Simple command-line interface for asking questions and viewing context.

---

## How It Works

1. **Document Loading:**
   - The `DoclingBookLoader` class loads and converts the PDF to markdown, extracting text and tables with OCR support.
2. **Text Splitting:**
   - The document is split into overlapping chunks using `RecursiveCharacterTextSplitter` for better context retrieval.
3. **Embeddings & Vector Store:**
   - Each chunk is embedded using HuggingFace's `all-MiniLM-L6-v2` model.
   - Chunks are indexed with FAISS for fast similarity search. The index is saved for future runs.
4. **Conversational QA Chain:**
   - A retriever fetches relevant chunks for each question.
   - The local LLM (via Ollama) answers questions using the retrieved context.
5. **User Interaction:**
   - Users ask questions in the terminal. The system displays both the answer and the supporting context.

---

## Setup & Installation

### 1. Clone the Repository

```bash
git clone <repository_url>
cd <repository_directory>
```

### 2. (Recommended) Create a Virtual Environment

```bash
python3 -m venv bookie
source bookie/bin/activate  # On Linux/macOS
# .\\bookie\\Scripts\\activate  # On Windows
```

### 3. Install Python Dependencies

```bash
pip install -r requirements.txt
```

### 4. Install Ollama (for Local LLM)

Follow instructions at [https://ollama.com/](https://ollama.com/) to install Ollama for your OS.

### 5. Download the Language Model

```bash
ollama pull mistral:latest
```

You can use other models supported by Ollama if desired (update the model name in `bookchat.py`).

---

## Usage

Run the script with the path to your PDF file:

```bash
python bookchat.py <path_to_your_pdf_file>
```

- Type your questions at the prompt.
- Type `quit` to exit.

---

## Example Session

```
$ python bookchat.py mybook.pdf
📚 Ready to answer questions about your PDF!
Type 'quit' to exit

❓ Ask a question: What is the main topic of chapter 2?
🔄 Processing your question...
... (retrieved context and answer displayed) ...
```

---

## Troubleshooting

- **Missing Dependencies:** Ensure all packages in `requirements.txt` are installed.
- **Ollama Not Running:** Start Ollama and ensure the model is downloaded.
- **Docling Issues:** See [Docling documentation](https://github.com/docling-org/docling) for help.
- **Performance:** First run may be slow for large PDFs (indexing). Subsequent runs are faster.

---

## .gitignore

- `*_faiss_index` — Vector store index files (auto-generated)
- `bookie/` — Virtual environment directory

---

## License

This project is licensed under the MIT License.
