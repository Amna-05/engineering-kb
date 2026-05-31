# .gitignore Reference

> Master reference for my stack: Python · FastAPI · Next.js · Docker · PostgreSQL
> Copy relevant sections into each project's root as `.gitignore`

---

## Full Template

```gitignore
# ============================================================
# SECRETS — ALWAYS IGNORE (non-negotiable)
# ============================================================
.env
.env.*
!.env.example
*.pem
*.key
*.p12
*.pfx
secrets/
credentials/
service-account*.json

# ============================================================
# PYTHON / FASTAPI
# ============================================================
__pycache__/
*.pyc
*.pyo
*.pyd
.Python
*.egg-info/
*.egg
dist/
build/
.venv/
venv/
env/
ENV/
.python-version

# Testing
.pytest_cache/
.coverage
coverage.xml
htmlcov/
.tox/

# Type checking / linting
.mypy_cache/
.ruff_cache/

# ============================================================
# NODE / NEXT.JS
# ============================================================
node_modules/
.next/
.nuxt/
out/
dist/
build/
*.log
npm-debug.log*
yarn-debug.log*
yarn-error.log*
.pnpm-debug.log*
.vercel
.turbo

# ============================================================
# DOCKER
# ============================================================
.docker/
docker-compose.override.yml

# ============================================================
# DATABASE
# ============================================================
*.sqlite
*.sqlite3
*.db
postgres-data/
pgdata/

# ============================================================
# OS
# ============================================================
.DS_Store
Thumbs.db
desktop.ini
*.swp
*.swo
*~

# ============================================================
# IDE / EDITORS
# ============================================================
.vscode/
!.vscode/extensions.json
.idea/
*.iml
*.sublime-project
*.sublime-workspace

# ============================================================
# LOGS & TEMP
# ============================================================
logs/
*.log
*.log.*
tmp/
temp/
uploads/
media/
```

---

## Notes

- Always commit `.env.example` — it tells teammates what vars are needed
- Never commit `postgres-data/` or any bind mount data folder
- `!.vscode/extensions.json` keeps the recommended extensions file (useful for teams)
- Add `docker-compose.override.yml` to gitignore — use it for local dev overrides only
