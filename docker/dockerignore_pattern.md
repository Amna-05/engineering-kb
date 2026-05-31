# ============================================================

### .dockerignore Master Reference

### Place this file at project root alongside Dockerfile

### Goal: keep image small, never leak secrets into image

### SECRETS — NEVER goes into an image

### ------------------------------------------------------------

.env
.env._
!.env.example
_.pem
\*.key
secrets/
credentials/

### ------------------------------------------------------------

### GIT

### ------------------------------------------------------------

.git/
.gitignore
.gitattributes

### ------------------------------------------------------------

### PYTHON

# ------------------------------------------------------------

**pycache**/
_.pyc
_.pyo
_.pyd
.venv/
venv/
env/
.pytest_cache/
.coverage
htmlcov/
.mypy_cache/
.ruff_cache/
_.egg-info/
dist/
build/

# ------------------------------------------------------------

# NODE / NEXT.JS

# ------------------------------------------------------------

node*modules/
.next/
out/
*.log
npm-debug.log\_

# ------------------------------------------------------------

# DOCKER (don't copy docker files into themselves)

# ------------------------------------------------------------

Dockerfile
Dockerfile._
docker-compose_.yml
.dockerignore

# ------------------------------------------------------------

# CI/CD

# ------------------------------------------------------------

.gitlab-ci.yml
.github/
.gitlab/

# ------------------------------------------------------------

# DOCS & README

# ------------------------------------------------------------

README.md
docs/
\*.md

# ------------------------------------------------------------

# IDE / OS

# ------------------------------------------------------------

.vscode/
.idea/
.DS_Store
Thumbs.db
\*.swp

# ------------------------------------------------------------

# TESTS (don't ship tests in production image)

# ------------------------------------------------------------

tests/
test/
**tests**/
_.test.py
_.spec.ts
coverage/

# ------------------------------------------------------------

# LOGS & TEMP

# ------------------------------------------------------------

logs/
\*.log
tmp/
temp/

# ============================================================

# QUICK NOTES

# ============================================================

# - .dockerignore works like .gitignore but for Docker build context

# - Smaller context = faster builds

# - Never let .env or keys get into an image layer (even if deleted later,

# they exist in the layer history)

# - Always have .env.example committed so team knows what vars are needed
