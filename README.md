# Local RAG System with Mistral and Ollama

A Retrieval-Augmented Generation (RAG) system that uses local Mistral model via Ollama for text generation, with FAISS for efficient vector search.

## Features

- Document processing for PDF, DOCX, and TXT files
- Text chunking with configurable size and overlap
- Vector embeddings using Google Gemini API
- Efficient similarity search with FAISS
- REST API with FastAPI
- Modern React frontend with Tailwind CSS
- Document upload and chat interface
- Context-aware responses with source attribution

## Prerequisites

- Python 3.8+
- Node.js 16+
- [Ollama](https://ollama.ai/) installed and running
- Mistral model downloaded in Ollama (run `ollama pull mistral`)

## Setup

1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd rag
   ```

2. Set up the backend:
   ```bash
   # Create and activate a virtual environment
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate

   # Install backend dependencies
   cd backend
   pip install -r requirements.txt
   cd ..
   ```

3. Set up the frontend:
   ```bash
   cd frontend
   npm install
   cd ..
   ```

4. Start the backend server:
   ```bash
   cd backend
   uvicorn main:app --reload
   ```

5. In a new terminal, start the frontend:
   ```bash
   cd frontend
   npm start
   ```

6. The application should now be running at `http://localhost:3000`
   ```
   GOOGLE_API_KEY=your_api_key_here
   ```

## Running the Application

### Backend

Start the FastAPI server:
```bash
uvicorn app.main:app --reload
```

The API will be available at `http://localhost:8000`

### Frontend

In a new terminal, start the React development server:
```bash
cd frontend
npm start
```

The frontend will be available at `http://localhost:3000`

## API Endpoints

- `GET /` - API information
- `GET /health` - Health check
- `POST /upload` - Upload and index a document
- `POST /query` - Query the RAG system
- `GET /documents/count` - Get document count
- `DELETE /documents` - Clear all documents (for testing)

## Example API Usage

### Upload a Document

```bash
curl -X 'POST' \
  'http://localhost:8000/upload' \
  -H 'accept: application/json' \
  -H 'Content-Type: multipart/form-data' \
  -F 'file=@document.pdf;type=application/pdf' \
  -F 'metadata={"title":"Example Document"};type=application/json'
```

### Query the RAG System

```bash
curl -X 'POST' \
  'http://localhost:8000/query' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
    "query": "What is this document about?",
    "top_k": 3
  }'
```

## Persisting FAISS Index

The FAISS index is automatically saved to the `indices` directory when documents are added. To persist the index between server restarts, make sure the `indices` directory exists and is writable.

## Frontend Features

- Drag and drop document upload
- Real-time chat interface
- Document management
- Responsive design
- Syntax highlighting for code blocks
- Source attribution for answers

## License

This project is licensed under the MIT License - see the LICENSE file for details.
