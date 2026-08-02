# PDF Toolbox

A web app for working with PDFs (compress, and more tools to come), built with a Flask backend and a lightweight frontend.

## Project structure

```
pdf_toolbox/
├─ backend/
│  ├─ venv/              # Python virtual environment (not committed)
│  ├─ uploads/            # Uploaded PDFs (not committed)
│  ├─ results/            # Processed output files (not committed)
│  ├─ app.py              # Flask app entry point
│  ├─ config.py           # App configuration (reads .env)
│  ├─ models.py           # SQLAlchemy models
│  ├─ requirements.txt    # Python dependencies
│  └─ .env                # Environment variables (not committed)
└─ frontend/               # Frontend files (HTML/CSS/JS)
```

## Tech stack

- **Backend:** Flask, Flask-SQLAlchemy, PyMuPDF, PyMySQL
- **Database:** MySQL
- **Frontend:** plain HTML/CSS/JS (for now)

## Getting started

### 1. Clone and enter the project

```bash
git clone <your-repo-url>
cd pdf_toolbox
```

### 2. Backend setup

```powershell
cd backend
python -m venv venv
.\venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

### 3. Configure environment variables

Create a `.env` file inside `backend/` (see `.env.example` if provided):

```
FLASK_APP=app.py
FLASK_ENV=development

DB_USER=pdf_user
DB_PASSWORD=your_password
DB_HOST=localhost
DB_PORT=3306
DB_NAME=pdf_toolbox

SECRET_KEY=change_this_to_a_random_secret
```

### 4. Set up the database

```sql
CREATE DATABASE pdf_toolbox CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
CREATE USER 'pdf_user'@'localhost' IDENTIFIED BY 'your_password';
GRANT ALL PRIVILEGES ON pdf_toolbox.* TO 'pdf_user'@'localhost';
FLUSH PRIVILEGES;
```

Then create the tables:

```powershell
python -c "from app import app, db; from models import Job, File, JobResult; app.app_context().push(); db.create_all(); print('Tables created')"
```

### 5. Run the backend

```powershell
flask run
```

Visit:
- `http://127.0.0.1:5000/` — health check
- `http://127.0.0.1:5000/health` — Flask + DB status check

## Roadmap

- [ ] PDF compression endpoint
- [ ] Simple upload UI in `frontend/`
- [ ] Additional PDF tools (merge, split, watermark, etc.)
- [ ] Docker Compose setup (Flask + MySQL)

## License

TBD
