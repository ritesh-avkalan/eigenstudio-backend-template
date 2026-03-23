# Deployment Guide
This guide explains how to deploy the `eigenplus-backend` FastAPI application in different environments: local, staging, and production. It also outlines required environment variables and how to connect to external services like the database and storage.

---

## 1. Overview
The backend is built with FastAPI and connects to a PostgreSQL database and optionally to an object storage service like AWS S3. The deployment process depends on where the backend is being hosted:

- Local development: run with `uvicorn`
- Cloud deployment: use EC2, ECS, or Docker container

---

## 2. Prerequisites
- PostgreSQL database (local or RDS)
- `.env` file with environment variables (see `.env.example`)
- (Optional) AWS S3 bucket for file uploads

---

## 3. Local Deployment
1. Clone the repo and enter the directory:
   ```bash
   git clone https://github.com/eigenstudio/eigenplus-backend.git
   cd eigenplus-backend
   ```

2. Create a virtual environment and install dependencies:
   ```bash
   python -m venv .venv
   source .venv/bin/activate
   pip install -r requirements.txt
   ```

3. Copy `.env.example` to `.env` and fill in the correct values:
   ```bash
   cp .env.example .env
   ```

4. Start the FastAPI server:
   ```bash
   uvicorn app.main:app --reload
   ```

5. Visit the API at:
   - `http://localhost:8000/docs` (Swagger UI)
   - `http://localhost:8000/redoc` (ReDoc UI)

---

## 4. Production Deployment (EC2 or Docker)
- Use `gunicorn` or `uvicorn` with `--host 0.0.0.0` and `--workers` flag for performance
- Run behind a reverse proxy like Nginx or use an ALB
- Use Docker for portability

### Docker Run Example:
```bash
docker build -t eigenplus-backend .
docker run -d --env-file .env -p 8000:8000 eigenplus-backend
```

---

## 5. Environment Variables
The following variables must be set in `.env` or provided in deployment secrets:

```ini
DATABASE_URL=postgresql://user:pass@hostname/dbname
JWT_SECRET_KEY=your_jwt_secret_key
S3_BUCKET_NAME=your-bucket-name  # Optional
AWS_ACCESS_KEY_ID=...
AWS_SECRET_ACCESS_KEY=...
```

---

## 6. Connecting to PostgreSQL
Make sure your backend can reach the database:
- Use `localhost` if local
- Use RDS endpoint if deployed
- Ensure the database is migrated via `eigenplus-database` repo using Alembic

---

## 7. Integration with Other Repos

| Repo          | Integration Notes                           |
|---------------|----------------------------------------------|
| `eigenplus-database`| Use Alembic migrations before deployment     |
| `eigenplus-common`  | Shared Python models (Pydantic schemas)      |
| `eigenplus-frontend`| Connects to backend APIs                     |
| `eigenplus-infra`   | Provisions EC2, RDS, S3, etc. using Terraform|

---

## 8. Post-Deployment Checklist
- [ ] API is up and accessible
- [ ] `/docs` route is reachable
- [ ] DB connection is working
- [ ] JWT secret is configured
- [ ] File uploads are writing to disk/S3 (if enabled)
- [ ] Logs are being written and monitored
- [ ] Health check route responds (`GET /health` if implemented)

---

This deployment setup ensures the backend service is production-ready, secure, and compatible with the rest of the eigenplus platform.