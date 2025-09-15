## Inkubator IT — FastAPI API Template

Standardized API template for projects in the Inkubator IT GitHub organization. This template is maintained by the DevOps team to unify stack choices, local development, containerization, and deployment conventions across client projects.

### Tech stack
- **Runtime**: Python 3.12+
- **Framework**: FastAPI
- **Dependency/Env tool**: `uv`
- **Containerization**: Docker

### Project structure
```
.
├─ app/
│  ├─ __init__.py
│  └─ main.py            # Application entry with a sample route
├─ Dockerfile            # Container image using uv for installs
├─ pyproject.toml        # Project metadata and dependencies
├─ uv.lock               # Resolved lockfile
├─ .env.example          # Example environment variables
└─ README.md
```

### Prerequisites
- **Python** 3.12+
- **uv** package manager
  - Install options:
    - macOS/Linux: `curl -LsSf https://astral.sh/uv/install.sh | sh`
    - Or via pipx: `pipx install uv`
- Optional: **Docker** (to build and run a container)

### Getting started (local development)
1) Create your local env file and adjust values:
```sh
cp .env.example .env
```

2) Install dependencies (creates a local `.venv` managed by uv):
```sh
uv sync
```

3) Run the API in dev mode (auto-reload):
```sh
uv run fastapi dev app/main.py --host 0.0.0.0 --port 8000
```

4) Open `http://localhost:8000` (or your `PORT`).

5) Production-style run (no reload):
```sh
uv run fastapi run app/main.py --host 0.0.0.0 --port 8000
```

Notes:
- If you prefer Uvicorn directly, you can use: `uv run uvicorn app.main:app --reload --host 0.0.0.0 --port 8000`.

### Environment variables
Duplicate `.env.example` to `.env` and update values. Do not commit `.env`.

- **CLIENT_URL**: Allowed client origin (configure CORS in your app as needed)

### API endpoints
- `GET /` → returns a simple JSON payload:
```json
{"message": "Hello, World!"}
```

### Run with Docker
Build the image:
```sh
docker build -t inkubatorit/fastapi-template .
```

Run the container (reads `.env`):
```sh
docker run --rm --env-file .env -p 8000:80 inkubatorit/fastapi-template
```

Notes:
- The container listens on port `80` (see `Dockerfile` CMD). The example maps your host `8000` to container `80`.

### Common commands
- **Install deps**: `uv sync`
- **Dev (reload)**: `uv run fastapi dev app/main.py --host 0.0.0.0 --port 8000`
- **Start (prod)**: `uv run fastapi run app/main.py --host 0.0.0.0 --port 8000`
- **Freeze lockfile**: `uv lock`
- **Add a dependency**: `uv add <package>`
- **Upgrade deps**: `uv sync --upgrade`

### Development notes
- This template uses `fastapi[standard]`, which provides the FastAPI CLI and common production extras.
- Consider adding code quality tools (e.g., Ruff, Black, mypy) as your project grows.

### Contributing
This template is maintained by the **Inkubator IT DevOps** team. Contributions and improvements are welcome via Pull Requests. For significant changes, please open an Issue for discussion first.

### Support
For questions or support, contact the Inkubator IT DevOps team.

### License
Copyright (c) Inkubator IT. All rights reserved.
