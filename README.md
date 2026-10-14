# Data Analytics Agent

A full-stack data analysis application that lets users upload datasets, run automated exploratory data analysis (EDA), generate charts, and produce AI-assisted insights.

This repository contains:
- a FastAPI backend for data processing, authentication, analysis orchestration, and job management
- a Vite + React + TypeScript frontend for the user experience
- background task processing with Celery and Redis
- optional AI-powered analysis using Anthropic/OpenAI models

---

## Project overview

The app is designed for workflows like:
- upload CSV or Excel files
- validate and process uploaded data
- generate EDA summaries and metadata
- create chart visualizations from numeric and categorical columns
- build AI-generated insight reports
- export or review analysis status through an API

---

## Tech stack

### Backend
- Python 3.10+
- FastAPI
- SQLAlchemy
- Pydantic
- Celery
- Redis
- Pandas / NumPy / SciPy
- Plotly
- OpenAI / LangChain / Anthropic integrations

### Frontend
- React
- Vite
- TypeScript
- Tailwind CSS
- shadcn/ui components
- React Router
- Recharts / Plotly for charts

---

## Repository structure

```text
Data-Analytics-Agent-main/
├── backend/
│   ├── app/
│   │   ├── agents/
│   │   ├── core/
│   │   ├── models/
│   │   └── routers/
│   ├── config.py
│   ├── main.py
│   ├── requirements.txt
│   └── jobs_data/
├── data-weaver-ai/
│   ├── src/
│   ├── public/
│   ├── package.json
│   └── vite.config.ts
├── docs/
│   └── DETAILED_FUNCTION_WORKFLOWS.md
├── runtime.txt
├── .gitignore
└── README.md
```

---

## Features

- File upload for CSV and Excel datasets
- Automated preprocessing and quality checks
- EDA metrics such as missing values, distributions, correlations, and summary statistics
- Chart generation for numeric and categorical data
- Analysis tracking and status APIs
- User authentication and JWT-based access control
- Background jobs for heavy processing tasks
- Export and dashboard-style reporting support

---

## Prerequisites

Before running the project, install:
- Python 3.10 or newer
- Node.js 20.x
- npm or pnpm
- Redis (for Celery task queue)

---

## Backend setup

1. Open a terminal in the `backend` folder.
2. Create and activate a virtual environment:

```bash
cd backend
python -m venv .venv
# Windows
.venv\Scripts\activate
# macOS/Linux
source .venv/bin/activate
```

3. Install Python dependencies:

```bash
pip install -r requirements.txt
```

4. Create a `.env` file in the `backend` folder with values similar to:

```env
DATABASE_URL=sqlite:///./data.db
JWT_SECRET=change-me-in-production
JWT_ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=60
ANTHROPIC_API_KEY=your_key_here
OPENAI_API_KEY=your_key_here
REDIS_URL=redis://localhost:6379
FRONTEND_URL=http://localhost:5173
```

5. Start the backend:

```bash
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

The API will be available at:
- http://localhost:8000
- Swagger docs: http://localhost:8000/docs
- OpenAPI schema: http://localhost:8000/openapi.json

---

## Frontend setup

1. Open a terminal in the `data-weaver-ai` folder.
2. Install dependencies:

```bash
cd data-weaver-ai
npm install
```

3. Run the frontend:

```bash
npm run dev
```

The frontend typically runs at:
- http://localhost:5173

---

## Running background tasks

If the application uses Celery background tasks, make sure Redis is running locally before starting workers:

```bash
redis-server
```

Then start a worker from the backend directory:

```bash
celery -A app.celery_app worker --loglevel=info
```

---

## Environment and configuration notes

- The backend settings are defined in `backend/app/core/config.py`.
- The project uses `.env` files for secrets and app configuration.
- In production, rotate JWT secrets and API keys and avoid using default values.
- The app is configured to run in development mode by default.

---

## Notes on project status

This repository is a working project scaffold and data-analysis application with API-driven workflows. Some modules are intentionally structured for extensibility and may require additional environment configuration or external services such as Redis and LLM providers for full functionality.

For deeper implementation details, see:
- `docs/DETAILED_FUNCTION_WORKFLOWS.md`

---

## License

This project does not currently include a license file. If you are planning to publish or share it publicly, add an appropriate license such as MIT or Apache 2.0.

---

## Contributing

To contribute:
1. fork the repository
2. create a feature branch
3. make changes and validate locally
4. submit a pull request with a clear summary

---

## Quick start summary

```bash
# Backend
cd backend
python -m venv .venv
.venv\Scripts\activate  # or source .venv/bin/activate
pip install -r requirements.txt
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000

# Frontend
cd ../data-weaver-ai
npm install
npm run dev
```

