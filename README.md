# Financial Document Analyzer

## Bugs Found and How They Were Fixed

- **Undefined LLM Variable:** Properly initialized the language model (`ChatOpenAI`) to fix startup errors.
- **Missing PDF Import:** Added the correct import for PDF loading (`PyPDFLoader`) to enable document processing.
- **Function Name Conflicts:** Renamed duplicate functions to avoid API endpoint issues.
- **Incorrect Tool Imports:** Removed incompatible decorators and adjusted tool functions for library compatibility.
- **API Startup Configuration:** Fixed `uvicorn` configuration for proper reload without warnings.
- **Missing Dependencies:** Updated `requirements.txt` with all necessary packages.
- **Documentation Typos:** Corrected `requirement.txt` to `requirements.txt`.

These fixes ensure the system runs smoothly and processes financial documents correctly.

---

## Setup and Usage Instructions

### Prerequisites

- Python 3.8+
- OpenAI API key
- (Optional) Serper API key for web search features

### Installation

1. Clone the repository:
    ```bash
    git clone https://github.com/yourusername/financial-document-analyzer.git
    cd financial-document-analyzer
    ```

2. Create and activate a virtual environment:
    ```bash
    python -m venv venv
    # Windows
    venv\Scripts\activate
    # macOS/Linux
    source venv/bin/activate
    ```

3. Install dependencies:
    ```bash
    pip install -r requirements.txt
    ```

4. Create a `.env` file in the root directory with:
    ```
    OPENAI_API_KEY=your_openai_api_key_here
    SERPER_API_KEY=your_serper_api_key_here  # optional
    ```

5. Start the server:
    ```bash
    python main.py
    ```

6. Verify the API is running:
    - Health check: `http://localhost:8000/health`
    - API docs: `http://localhost:8000/docs`

---

## API Documentation

### Base URL


### Endpoints

#### GET `/`

- Returns API status.

```json
GET /health

System health check.

Response:

{
  "status": "healthy",
  "api": "operational",
  "endpoints": {
    "analyze": "/analyze - POST endpoint for document analysis",
    "health": "/health - System health check"
  }
}

POST /analyze

Analyze a financial PDF document.

Parameters:

file (required): PDF file to analyze

query (optional): Analysis question (default: general analysis)

Example cURL:

curl -X POST "http://localhost:8000/analyze" \
  -H "Content-Type: multipart/form-data" \
  -F "file=@your-file.pdf" \
  -F "query=Analyze the financial health of the company"


Success response:

{
  "status": "success",
  "query": "Analyze the financial health of the company",
  "filename": "your-file.pdf",
  "analysis": "Detailed financial analysis here...",
  "agents_used": ["document_verifier", "financial_analyst"],
  "file_id": "uuid-string"
}

POST /analyze-advanced

Advanced multi-agent analysis.

Parameters:

file (required): PDF document to analyze

query (optional): Analysis question

include_investment_advice (boolean, default: true)

include_risk_assessment (boolean, default: true)

🧪 Testing

Use the Swagger UI at http://localhost:8000/docs
 for interactive testing.

Test endpoints with the cURL commands above.

Verify system health at http://localhost:8000/health
.

🏗️ Development Notes

Built with FastAPI and Uvicorn.

Multi-agent orchestration via CrewAI.

PDF processing using LangChain's PyPDFLoader.

Uses OpenAI GPT-3.5-turbo model.

Handles input validation and errors gracefully.

Temporary files are cleaned up automatically after processing.
