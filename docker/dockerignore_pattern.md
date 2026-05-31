# .dockerignore Reference

> Place this file at project root alongside your Dockerfile.
> Goal: smaller image, faster builds, no secrets ever leaking into layers.

---

## Full Template

```dockerignore
# ============================================================
# SECRETS — NEVER goes into an image
# ============================================================
.env
.env.*
!.env.example
*.pem
*.key
secrets/
credentials/

# ============================================================
# GIT
# ============================================================
.git/
.gitignore
.gitattributes

# ============================================================
# PYTHON
# ============================================================
__pycache__/
*.pyc
*.pyo
*.pyd
.venv/
venv/
env/
.pytest_cache/
.coverage
htmlcov/
.mypy_cache/
.ruff_cache/
*.egg-info/
dist/
build/

# ============================================================
# NODE / NEXT.JS
# ============================================================
node_modules/
.next/
out/
*.log
npm-debug.log*

# ============================================================
# DOCKER FILES (don't copy into themselves)
# ============================================================
Dockerfile
Dockerfile.*
docker-compose*.yml
.dockerignore

# ============================================================
# CI/CD
# ============================================================
.gitlab-ci.yml
.github/
.gitlab/

# ============================================================
# DOCS
# ============================================================
README.md
docs/
*.md

# ============================================================
# IDE / OS
# ============================================================
.vscode/
.idea/
.DS_Store
Thumbs.db
*.swp

# ============================================================
# TESTS (don't ship in production image)
# ============================================================
tests/
test/
__tests__/
coverage/

# ============================================================
# LOGS & TEMP
# ============================================================
logs/
*.log
tmp/
temp/
```

---

## Key Rules

- Even if you `RUN rm secret.env` in a later layer, it still exists in the earlier layer's history — always exclude upfront
- `node_modules/` must be excluded — always reinstall inside the container
- Excluding `tests/` keeps production images lean
- `.git/` exclusion alone can save 50-100MB on older repos
