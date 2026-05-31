# ============================================================

# .gitignore Master Reference

# Stack: Python · FastAPI · Next.js · Docker · PostgreSQL

# Copy what you need into your project root

# ============================================================

# ------------------------------------------------------------

# SECRETS — ALWAYS IGNORE (non-negotiable)

# ------------------------------------------------------------

.env
.env._
!.env.example # keep the example template
_.pem
_.key
_.p12
_.pfx
secrets/
credentials/
service-account_.json

# ------------------------------------------------------------

# PYTHON / FASTAPI

# ------------------------------------------------------------

**pycache**/
_.py[cod]
_.pyo
_.pyd
.Python
_.egg-info/
\*.egg
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

# Alembic (keep versions folder, ignore local db state)

# alembic/versions/ ← DO NOT ignore this

# Type checking

.mypy_cache/
.ruff_cache/

# ------------------------------------------------------------

# NODE / NEXT.JS

# ------------------------------------------------------------

node_modules/
.next/
.nuxt/
out/
dist/
build/
_.log
npm-debug.log_
yarn-debug.log*
yarn-error.log*
.pnpm-debug.log\*
.vercel
.turbo

# ------------------------------------------------------------

# DOCKER

# ------------------------------------------------------------

.docker/
docker-compose.override.yml # local overrides only

# ------------------------------------------------------------

# DATABASE

# ------------------------------------------------------------

_.sqlite
_.sqlite3
\*.db
postgres-data/
pgdata/

# ------------------------------------------------------------

# OS

# ------------------------------------------------------------

.DS_Store
Thumbs.db
desktop.ini
_.swp
_.swo
\*~

# ------------------------------------------------------------

# IDE / EDITORS

# ------------------------------------------------------------

.vscode/
!.vscode/extensions.json # keep recommended extensions
.idea/
_.iml
_.sublime-project
\*.sublime-workspace

# ------------------------------------------------------------

# LOGS

# ------------------------------------------------------------

logs/
_.log
_.log.\*

# ------------------------------------------------------------

# MISC

# ------------------------------------------------------------

.cache/
tmp/
temp/
uploads/ # user uploaded files
media/ # if storing locally
