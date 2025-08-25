# FastAPI Project Template

Base template used for each project in **90 Projects in 90 Days**.
Index site: https://90projects.marekstepan.cz

## Quickstart
1) Create and activate a virtual environment
   macOS/Linux:
     python3 -m venv .venv
     source .venv/bin/activate
   Windows (PowerShell):
     python -m venv .venv
     .\.venv\Scripts\Activate.ps1

2) Install dependencies
   python -m pip install --upgrade pip
   pip install -r requirements.txt

3) Run the app (dev mode with auto-reload)
   python -m uvicorn app.main:app --reload
   Open http://127.0.0.1:8000

## Project layout
app/
  __init__.py
  main.py               # contains: app = FastAPI()
templates/
  index.html            # Jinja template
static/
  style.css
requirements.txt
Procfile                # start command for PaaS
tooling-diary.md
README.md
LICENSE

## Notes (templates & static)
- Static files are mounted in main.py:
  app.mount("/static", StaticFiles(directory="static"), name="static")
- Reference static in templates with Jinja:
  <link rel="stylesheet" href="{{ url_for('static', path='style.css') }}">

## Deploy (generic PaaS)
- Build command:  pip install -r requirements.txt
- Start command:  uvicorn app.main:app --host 0.0.0.0 --port $PORT
- Set environment variables in the PaaS dashboard (do not commit secrets).
- Optional: pin Python version for builders (some platforms read this):
  echo "python-3.12.5" > runtime.txt
  git add runtime.txt && git commit -m "chore: pin python" && git push

## Using this template
- GitHub UI: click “Use this template” → create repo (e.g., project-01-hello-web)
- GitHub CLI:
  gh repo create <USER>/project-XX-... --public --template <USER>/fastapi-project-template

## Troubleshooting
- ModuleNotFoundError: No module named 'app'
  • Run from the project root (the folder that contains the app/ directory).
  • Ensure app/__init__.py exists.
  • Or, if you are inside the app/ folder, run: python -m uvicorn main:app --reload

- macOS Apple Silicon arch mismatch (e.g., pydantic_core x86_64 vs arm64)
  • Recreate the venv and reinstall: 
      rm -rf .venv
      python3 -m venv .venv
      source .venv/bin/activate
      python -m pip install --upgrade pip
      pip install -r requirements.txt
  • Run the server via the venv interpreter:
      python -m uvicorn app.main:app --reload

## Environment variables
- Do not commit real secrets. Keep .env files out of git.
- Provide an example file for collaborators:
  .env.example

## License
MIT — see LICENSE.
