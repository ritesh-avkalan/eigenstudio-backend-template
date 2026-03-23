# ESD Backend
This is the backend service for the EigenSim (ESD) simulation platform. It is built using FastAPI and connects to a PostgreSQL database to handle file uploads and metadata storage.

---
## Requirements
- Python 3.11+
- PostgreSQL running locally or remotely
- Database already migrated (from `esd-database`)
- Backend virtual environment

---
## Project Setup
1. **Clone the repo and create a virtual environment**

```bash
git clone https://github.com/YOUR_ORG/esd-backend.git
cd esd-backend
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
````

2. **Create .env file**
```
DATABASE_URL=postgresql+psycopg2://postgres:postgres@localhost:5432/esd
```

> Make sure the database is already set up and migrated using esd-database.

---

## **Run the Backend Server**
```
uvicorn app.main:app --reload
```

- API Docs: [http://localhost:8000/docs](http://localhost:8000/docs)
- You can test the /files/ upload and listing endpoints

---

## **Example Endpoints**

| **Method** | **Route** | **Description**     |
| ---------- | --------- | ------------------- |
| POST       | /files/   | Upload a file       |
| GET        | /files/   | List uploaded files |

---

## **Folder Structure**

```
esd-backend/
├── app/
│   ├── main.py            # FastAPI entrypoint
│   ├── routes/            # API routes
│   ├── models/            # SQLAlchemy models
│   ├── schemas/           # Pydantic models (I/O)
│   ├── services/          # Helper functions (file storage, etc.)
│   ├── core/              # DB config and connection
│   └── dependencies/      # Common route dependencies
├── uploads/               # Where uploaded files are saved
├── requirements.txt       # Python dependencies
├── .env.example           # Sample environment config
└── README.md              # This file
```

---

## **Notes**

- Make sure your database is running before starting the backend.
- This service only works if the database schema (via esd-database) is set up.
- You can later add user authentication, S3 upload, and simulation endpoints.