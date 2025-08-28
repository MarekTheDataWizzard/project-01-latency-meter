# Project 1 — Latency Meter

Live: https://p01.90projects.marekstepan.cz  
Index: https://90projects.marekstepan.cz

FastAPI + Chart.js app that measures round-trip latency to `/api/ping` and charts it live (avg / p95 / min / max). Includes `/healthz` for health checks.

## Run locally
python -m venv .venv
source .venv/bin/activate          # Windows: .\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -r requirements.txt
python -m uvicorn app.main:app --reload
# open http://127.0.0.1:8000

## Project layout
app/
  __init__.py
  main.py           # app = FastAPI(); mounts /static; routes /, /api/ping, /healthz
templates/
  index.html        # Tailwind + Chart.js UI
static/
  style.css
requirements.txt
apprunner.yaml      # runtime: python311; pre-run installs; port 8080
LICENSE
README.md

## Deploy — AWS App Runner (from source)
- Automatic deployments from GitHub (main branch)
- Build: handled via apprunner.yaml
- Start: uvicorn app.main:app --host 0.0.0.0 --port 8080
- Health check path: /healthz
- Custom domain: p01.90projects.marekstepan.cz (CNAME → *.awsapprunner.com + ACM validation CNAMEs)

## Notes
- No secrets in git. Use App Runner env vars / AWS SSM / Secrets Manager.
- If port conflicts locally: run with --port 8001.

## License
MIT — see LICENSE.
