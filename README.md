## SEO Optimizer Agent

A Flask-based SEO analysis microservice that scores and analyzes content for keywords, readability, headings, meta title quality, and overall SEO quality. Designed as a worker agent in a Supervisor–Worker architecture, but can also be used standalone through its REST API and web UI.

---

## Features

- **SEO scoring (0–100)** based on:
  - Keyword density and usage
  - Readability (Flesch Reading Ease + grade)
  - Meta title quality (length, presence)
  - Heading structure (H1/H2/H3)
  - Content length and structure
- **Prioritized recommendations**
  - 🔴 Critical, ⚠️ Important, 💡 Suggestions
- **Memory system**
  - Short-term: in-memory sessions & results
  - Long-term: JSON archive + pattern statistics
- **API + Swagger UI**
  - JSON REST API
  - Swagger docs at `/api/docs`
- **Simple Supervisor integration**
  - Health, register, analyze, status endpoints

---

## Quick Start

# 1. Go to project
cd seo-optimizer-agent

# 2. (Optional) Create venv
python -m venv venv
venv\Scripts\activate  # on Windows

# 3. Install dependencies
pip install -r requirements.txt

# 4. Run the agent
python app.py- Agent runs at: `http://localhost:5000`
- Swagger UI: `http://localhost:5000/api/docs`
- Web UI (dashboard): `http://localhost:5000/ui`

---

## Main Endpoints

- `GET /health` – Health check
- `POST /register` – Register with a supervisor
- `POST /analyze` – Analyze content for SEO
- `GET /status` – Agent statistics & memory usage
- `GET /history/<task_id>` – Get previous analysis by task ID

Example analyze request:

{
  "task_id": "task_001",
  "task_type": "analyze_content",
  "content": {
    "title": "SEO Best Practices for 2025",
    "body": "Your article content here...",
    "target_keywords": ["SEO", "optimization", "ranking"],
    "url": "https://example.com/article"
  },
  "options": { "detailed_analysis": true }
}---

## Supervisor Integration (High Level)

A supervisor typically:

1. `GET /health` – Check if agent is healthy
2. `POST /register` – Register the agent and store its capabilities
3. `POST /analyze` – Send tasks for SEO analysis
4. `GET /status` – Monitor performance and usage

See `sample_supervisor.py` for a working example.

---

## Project Structure (Core Files)

- `app.py` – Flask app, API endpoints
- `seo_analyzer.py` – SEO scoring & recommendations
- `memory_manager.py` – Short/long-term memory
- `swagger.yaml` – OpenAPI spec
- `static/`, `templates/` – Web UI (dashboard, status, history)

---

## License

Educational project for a Software Project Management course (FAST-NUCES Islamabad, 7th Semester).
