# Local Environment & Security Guide

This document explains how to set up the local development environment and manage environment variables securely. It also includes best practices for handling credentials and secrets.

---

## 1. Setting Up the Local Environment
1. **Clone the repository:**
   ```bash
   git clone https://github.com/eigenstudio/eigenplus-backend.git
   cd eigenplus-backend
   ```

2. **Create and activate a virtual environment (optional but recommended):**
   ```bash
   python -m venv .venv
   source .venv/bin/activate  # On Windows: .venv\Scripts\activate
   ```

3. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Copy the environment file:**
   ```bash
   cp .env.example .env
   ```

5. **Run the development server:**
   ```bash
   uvicorn app.main:app --reload
   ```

6. **Access the API:**
   Visit `http://localhost:8000/docs` for the interactive API documentation.

---

## 2. Environment Variables
All configuration and secrets should be stored in the `.env` file. **Do not commit actual `.env` files to Git.**

### Example `.env` settings:
```ini
DATABASE_URL=postgresql://postgres:postgres@localhost:5432/eigenplus
S3_BUCKET_NAME=eigenplus-dev
JWT_SECRET_KEY=supersecretkey123
```

Use a `.env.example` template to share expected keys without sensitive values.

---

## 3. Best Practices for Managing Secrets
- **Do not commit `.env` files or credentials to version control.**
- Use `.env` files only for development. Use secure environment variable management for staging/production.
- In CI/CD and deployment environments, use:
  - GitHub Secrets
  - AWS Systems Manager (SSM) or Secrets Manager
  - Vercel/Netlify Environment UI
- Never hardcode secrets, tokens, passwords, or access keys in source files.

---

## 4. Secure Development Tips
- Validate all incoming data using Pydantic schemas
- Use role-based access control for protected endpoints
- Limit CORS settings in production
- Enable HTTPS in production deployments
- Sanitize user-generated content if rendering it
- Monitor for exposed secrets using tools like `truffleHog` or `git-secrets`

---

## 5. Common Security Mistakes to Avoid
- Forgetting to add `.env` to `.gitignore`
- Pushing test secrets to GitHub
- Using the same secret in dev and prod
- Logging sensitive data (tokens, passwords)

---

Following these environment and security practices helps you work locally with confidence and deploy securely at scale.