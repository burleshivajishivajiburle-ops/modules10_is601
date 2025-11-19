## FastAPI Calculator

FastAPI app that serves:
- A small calculator UI + JSON endpoints (`/add`, `/subtract`, `/multiply`, `/divide`).
- A secure SQLAlchemy `User` model with hashed passwords, JWT helpers, and Pydantic schemas.

### What we completed
- Renamed the SQLAlchemy `User` column to `password_hash`, aligned the ORM, schemas, and auth dependencies, and updated the tests.
- Fixed Docker by trimming the build context with `.dockerignore` and mounting the Postgres 18 volume at `/var/lib/postgresql`.
- Verified the stack with `docker compose up` and end-to-end pytest runs (unit, integration, Playwright e2e) after installing browsers.
- Simplified this README and documented the Docker Hub image plus local workflow so the assignment rubric steps are easy to follow.

### Assignment checkpoints
- ✅ Local test instructions (see section 4) walk through activating the venv and running `pytest -q`.
- ✅ Docker Hub section links directly to the published image for quick pulls.

### 1. Local setup
```bash
cd assignmentsqla
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt
```

### 2. Run everything with Docker (recommended)
```bash
docker compose up -d
```
- App: http://localhost:8000
- Postgres: exposed on localhost:5432
- pgAdmin: http://localhost:5050 (admin@example.com / admin)

Stop with `docker compose down` (add `-v` to reset the DB volume).

### 3. Run the app without Docker (needs Postgres running)
```bash
source venv/bin/activate
uvicorn main:app --reload
```
Override `DATABASE_URL` in `.env` if you are not using the Dockerized Postgres.

### 4. Tests
```bash
source venv/bin/activate
pytest -q
```
Playwright tests require one-time browser install: `playwright install --with-deps`.

### 5. Docker Hub image
```bash
docker pull shivajiburle/asignmentsqlaa:latest
docker run -p 8000:8000 shivajiburle/asignmentsqlaa:latest
```
Docker Hub repo: https://hub.docker.com/r/shivajiburle/asignmentsqlaa

That’s it—clone, install requirements, run Docker (or uvicorn), and use pytest to verify changes.
