# bookchat (ask questions to a book to retrieve information)

Feed books to a local LLM to ask questions about the book. The LLM will answer by referencing the parts of the book where the info comes from and explain concepts. It is basically a simple RAG (Retrieval-Augmented Generation).

** the book needs to be a pdf file **

## Prerequisites

- Python 3.x
- Ollama running locally (default endpoint: http://localhost:11434)

More info about ollama on their webpage.

## Setup

1. Install the required dependencies:
```bash
pip install -r requirements.txt
```

2. Ensure Ollama is running a language model locally with the API endpoint available. 

You can also run the server at the terminal to see what is happening (ollamawise) in real-time:

```bash
ollama serve
```

## Usage

Start chatting with any PDF book:
```bash
python bookchat.py path/to/your/textbook.pdf
```

The system will:
1. Process your book. It may take A LOT of time according to how long the book is...
2. Create a knowledge base (first run only)
3. Save the processed data for faster future access
4. Start an interactive chat session

## More details

The script uses Docling from IBM to chunk the book and transform it to markdown for the LLM to process. More info on this at: https://docling-project.github.io/docling/ 
