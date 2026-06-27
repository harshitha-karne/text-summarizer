# Text Summarizer Minor Project

An **ML-based text summarization project** with a lightweight web interface, built using **FastAPI**, **Hugging Face Transformers**, and a locally saved **T5** model. The project combines machine learning and web development to accept long text or dialogue input from a browser UI and return a concise generated summary.

## Features

- Clean browser interface for entering text
- FastAPI backend with a JSON summarization endpoint
- T5 transformer model loaded from `saved_summary_model`
- Automatic CPU, CUDA, or Apple MPS device selection
- Basic input cleaning before summarization
- Notebook included for model training or experimentation

## Project Structure

```text
text summarizer minor/
|-- app.py                    # FastAPI application and summarization logic
|-- index.html                # Frontend UI
|-- text_summarizer.ipynb     # Notebook used for training/experiments
|-- saved_summary_model/      # Saved tokenizer and model files
|-- results/                  # Training/evaluation outputs
|-- samsum-train.csv          # Training dataset
|-- samsum-test.csv           # Test dataset
|-- samsum-validation.csv     # Validation dataset
|-- requirements.txt          # Python dependencies
`-- README.md                 # Project documentation
```

## Tech Stack

- Python
- FastAPI
- Uvicorn
- PyTorch
- Hugging Face Transformers
- SentencePiece
- HTML, CSS, and JavaScript

## Setup Instructions

### 1. Clone or Open the Project

Open the project folder:

```bash
cd "text summarizer minor"
```

### 2. Create a Virtual Environment

```bash
python -m venv venv
```

Activate it on Windows:

```bash
venv\Scripts\activate
```

Activate it on macOS/Linux:

```bash
source venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Check the Saved Model

Make sure the `saved_summary_model` folder exists in the project root. The app loads the model and tokenizer from this folder:

```python
T5ForConditionalGeneration.from_pretrained("./saved_summary_model")
T5Tokenizer.from_pretrained("./saved_summary_model")
```

### 5. Run the Application

```bash
uvicorn app:app --reload
```

Open this URL in your browser:

```text
http://127.0.0.1:8000
```

## API Usage

The app provides a POST endpoint for summarization.

### Endpoint

```http
POST /summarize/
```

### Request Body

```json
{
  "dialogue": "Your long text or conversation goes here."
}
```

### Response

```json
{
  "summary": "Generated summary text."
}
```

## How It Works

1. The user enters text in the web page.
2. JavaScript sends the text to the FastAPI backend.
3. The backend cleans the input text.
4. The tokenizer converts the text into model input tokens.
5. The T5 model generates a short summary.
6. The summary is returned and displayed on the page.

## Model Details

This project uses a locally saved T5 sequence-to-sequence model. T5 is useful for text-to-text NLP tasks such as summarization, translation, and question answering.

The generation settings used in `app.py` are:

- Maximum input length: `512`
- Maximum summary length: `150`
- Beam search: `4` beams
- Early stopping: enabled

## Dataset

The project includes SAMSum dataset CSV files:

- `samsum-train.csv`
- `samsum-validation.csv`
- `samsum-test.csv`

These files are commonly used for dialogue summarization experiments.

## Notes

- Keep `saved_summary_model` in the project root before running the app.
- If PyTorch with GPU support is installed and CUDA is available, the app will use GPU automatically.
- If no GPU is available, the app will run on CPU.
- The first summary may take longer because the model needs to load into memory.

## Author

Text Summarizer Minor Project
