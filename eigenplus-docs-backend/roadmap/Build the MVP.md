---
Date: 2025-07-10
assigned to:
  - abhi
description:
---
Perfect — here’s what a clean **MVP backend** for your simulation platform should support, based on everything you’ve shared so far.

---

## **✅ MVP Goal: File-based Simulation App**
> Let users upload mesh files, store them, launch simulations, and view results.

---

## **✅ MVP Features & APIs**

|**Domain**|**MVP Capabilities**|
|---|---|
|**Users**|No login system for now (just basic uploaded_by field)|
|**Projects**|Users can organize files under projects|
|**Files**|Upload files (e.g. .msh) → saved in S3 → DB stores metadata|
|**Jobs**|Backend triggers a simulation job (simulated by dummy function)|
|**Results**|List result files (PDF, CSV, etc.) or logs linked to a job|
|**Health**|Expose /health endpoint for deployment readiness|

---

## **✅ MVP Database Models (already in eigenplus-database)**

| **Table**     | **Fields (Simplified)**                                   |
| ------------- | --------------------------------------------------------- |
| project_files | id, file_name, uploaded_by, file_url, uploaded_at         |
| projects      | id, team_id, name, created_at, description                |
| jobs          | id, simulation_id, status, started_at, finished_at, logs  |
| results       | id, simulation_id, file_url, created_at                   |
| simulations   | id, mesh_id, physics_type, status, created_by, timestamps |

---

## **✅ Tech & Decisions for MVP**

|**Layer**|**Tech / Approach**|
|---|---|
|**Auth**|❌ No auth for MVP (just simulate uploaded_by)|
|**Storage**|✅ Local storage in /uploads/ folder (S3 later)|
|**Jobs**|✅ Python subprocess / dummy sleep + log|
|**DB Access**|✅ SQLAlchemy ORM, reuse models from eigenplus-database|
|**API**|✅ FastAPI with auto-generated docs at /docs|
|**CI**|✅ GitHub Actions to run lint + test on PRs|
|**Test**|✅ Basic pytest test on file upload and list|

---

## **🧱 API Endpoints You Need**

|**Endpoint**|**Method**|**Description**|
|---|---|---|
|/files|POST|Upload a file (returns metadata)|
|/files|GET|List uploaded files|
|/jobs|POST|Start a dummy simulation job|
|/jobs|GET|List jobs + status|
|/results|GET|Get result metadata or file URLs|
|/health|GET|Simple ping to confirm backend is alive|

---

## **🧠 Next Steps**

  

Now that the MVP is scoped, I’ll generate:

1. ✅ Folder structure for eigenplus-backend
2. ✅ Route files with stubbed handlers (files.py, jobs.py, etc.)
3. ✅ Models and schemas
4. ✅ Minimal services (file saving, dummy job runner)
5. ✅ A working example endpoint

  

Would you like me to start generating the code in steps now?