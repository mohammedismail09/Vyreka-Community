# Vyreka Community

Vyreka Community
This project uses a Django backend inside the `backend/` folder and a React + Vite frontend inside `frontend/`. The frontend calls Django APIs for team members, events, and contact form submissions, so both servers must run together during local development.

## Project structure

```text
Vyreka-Community/
├── backend/       # Django API (Python, PostgreSQL, Serverless Runtime)
│   ├── manage.py
│   ├── requirements.txt
│   └── .env
└── frontend/      # React UI (Vite, TypeScript, Tailwind CSS)
```
- Frontend: React + Vite deployed to Vercel (Static Web Hosting & Global CDN).

- Backend: Django deployed to Vercel (Python Serverless Functions Runtime).

- Database: PostgreSQL hosted on Neon.tech (Serverless Cloud Postgres).

🛠️ Tech Stack

Frontend
- Framework: React 18 (TypeScript)
- Build Tool: Vite
- Styling: Tailwind CSS

Backend
- Framework: Django 5.x
- Database Engine: PostgreSQL
- Dependencies: dj-database-url, psycopg2-binary, django-cors-headers, python-dotenv

Prerequisites
- Ensure you have the following installed on your local system:
- Node.js (v18+) & npm
- Python (3.10+)
- PostgreSQL Engine (Running locally on port 5432)

## What runs where
- Django runs the backend API and admin panel from `backend/`.

- React runs the frontend from `frontend/.`

- The frontend uses `VITE_BACKEND_URL` to connect to Django.

## 1) Clone the project

```bash
git clone <your-repo-url>
cd Vyreka-Community
```

## 2) Create `.env`

Navigate to the `backend/` directory and create a `.env` file by copying `.env.example`. The backend reads database connection parameters, email settings, and debug statuses from this file.

```bash
cp .env.example .env
```
If you are on Windows and `cp` does not work, create `.env` manually inside the backend/ folder and paste the values from `.env.example`.

Important:

Set your local or cloud PostgreSQL connection string under `DATABASE_URL`.

Fill `EMAIL_HOST_USER` and `EMAIL_HOST_PASSWORD` in your real `.env` file.

Use a Gmail App Password for `EMAIL_HOST_PASSWORD`, not your normal Gmail password.

Keep `.env` private and never commit it.

## 3) Backend setup

Navigate to the backend/ folder to create your Python virtual environment and install dependencies.

### Windows PowerShell

```bash
cd backend
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

### Windows CMD

```bash
cd backend
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
```

### macOS / Linux

```bash
cd backend
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Run migrations to set up your PostgreSQL tables:

```bash
python manage.py migrate
```

Optional: create an admin user:

```bash
python manage.py createsuperuser
```

Start Django:

```bash
python manage.py runserver
```

The backend will run at:

```text
http://127.0.0.1:8000/
```

## 4) Frontend setup

Open a second terminal and navigate into the frontend/ folder. The frontend has its own dependencies and must be started separately from Django.

```bash
cd frontend
npm install
npm run dev
```

The frontend will usually run at:

```text
http://127.0.0.1:5173/
```

## 5) Run in two terminals

### Terminal 1 — Django backend

```bash
cd VYREKA_COMMUNITY
.venv\Scripts\activate   # Windows example
python manage.py runserver
```

### Terminal 2 — Frontend

```bash
cd VYREKA_COMMUNITY/frontend
npm install
npm run dev
```

## 6) Open the app

- Frontend: `http://127.0.0.1:5173/`
- Backend: `http://127.0.0.1:8000/`
- Django admin: `http://127.0.0.1:8000/admin/`

## Common local workflow

1. Common local workflow
Navigate to `backend/` and activate `.venv`.

2. Run Django from the `backend/` directory.

3. Open a second terminal.

4. Run the frontend from `frontend/`.

5. Edit backend files in your app subfolders (e.g., `home/`).

6. Edit frontend files in `frontend/src/`.

## Deployment note

For frontend deployment on Vercel, set `VITE_BACKEND_URL` in the hosting dashboard environment variables configuration panel pointing to your live deployed backend. Vite exposes only `VITE_` prefixed variables to frontend code and injects them dynamically at build time.

For backend deployment on Vercel, select the same repository but set the Root Directory setting explicitly to `backend/`. Add the Django and environment variables inside the backend project dashboard separately, including `DATABASE_URL`, `SECRET_KEY`, `DEBUG`, email settings, CORS settings, and CSRF trusted origins rules.
