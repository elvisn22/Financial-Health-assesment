## Financial Health Assessment Tool

A full-stack platform for assessing the financial health of small and medium enterprises (SMEs).  
It ingests financial statements and business metrics, analyzes them with Python + pandas, and exposes an API and web UI for interactive insights and recommendations.

### High-Level Architecture

- **Backend (`backend/`)**: FastAPI service in Python for:
  - Uploading CSV / XLSX / PDF (text-based) financial data
  - Parsing data into pandas DataFrames
  - Calculating financial ratios and health scores
  - Generating narrative insights via an LLM (OpenAI-compatible)
  - Persisting data and results in PostgreSQL
- **Frontend (`frontend/`)**: React single-page app for:
  - Secure login
  - Uploading financial files
  - Viewing dashboards with health score, ratios, and recommendations
- **Database**: PostgreSQL (recommended to run via Docker).

### Tech Stack

- **Backend**: Python 3.10+, FastAPI, pandas, SQLAlchemy, PostgreSQL, pdfplumber
- **Frontend**: React + TypeScript + Vite
- **LLM**: OpenAI-compatible HTTP API (model configurable via env)
- **Security**:
  - JWT-based authentication
  - Encryption of sensitive financial payloads at rest using Fernet (symmetric encryption)
  - HTTPS recommended via reverse proxy (e.g. Nginx) in production

### Getting Started (Development)

1. **Clone or open the project directory**

2. **Backend setup**

   ```bash
   cd backend
   python -m venv .venv
   .venv\Scripts\activate  # On Windows
   pip install -r requirements.txt

   # Set environment variables (example)
   set DATABASE_URL=postgresql+psycopg2://user:password@localhost:5432/financial_health
   set SECRET_KEY=your-jwt-secret
   set ENCRYPTION_KEY=your-fernet-key-base64
   set OPENAI_API_KEY=your-openai-key

   uvicorn app.main:app --reload
   ```

3. **Frontend setup**

   ```bash
   cd frontend
   npm install
   npm run dev
   ```

4. Open the printed local URL from the frontend dev server (e.g. `http://localhost:5173`) to use the app.

### Notes

- This is a reference implementation you can extend for the hackathon:
  - Add real banking/payment API integrations in `backend/app/integrations/`
  - Enhance the scoring engine in `backend/app/services/assessment.py`
  - Customize UI branding/theme in `frontend/src/styles/`

