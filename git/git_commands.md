# Git & GitHub Reference

> Personal runbook — commands, workflows, and patterns I actually use.
> Last updated: 2026

---

## Table of Contents

- [Setup & Config](#setup--config)
- [Daily Workflow](#daily-workflow)
- [Branching](#branching)
- [Staging & Committing](#staging--committing)
- [Undoing Things](#undoing-things)
- [Rebase Workflow](#rebase-workflow)
- [Remote & GitHub](#remote--github)
- [Stashing](#stashing)
- [Logs & Inspection](#logs--inspection)
- [Tags](#tags)
- [GitHub CLI](#github-cli)
- [.gitignore Patterns](#gitignore-patterns)
- [Troubleshooting](#troubleshooting)

---

## Setup & Config

```bash
# Identity
git config --global user.name "Amna"
git config --global user.email "your@email.com"

# Default branch name
git config --global init.defaultBranch main

# Set VS Code as default editor
git config --global core.editor "code --wait"

# Rebase on pull by default (recommended)
git config --global pull.rebase true

# View all global config
git config --global --list

# View config for current repo
git config --list
```

---

## Daily Workflow

```bash
# Clone a repo
git clone https://github.com/user/repo.git
git clone git@github.com:user/repo.git          # SSH

# Clone into specific folder
git clone https://github.com/user/repo.git my-folder

# Pull latest (rebase keeps history clean)
git pull --rebase

# Pull specific branch
git pull origin main --rebase

# Check status
git status
git status -s                                    # short format

# See what changed
git diff                                         # unstaged changes
git diff --staged                                # staged changes
git diff main..feature-branch                   # between branches
```

---

## Branching

```bash
# List branches
git branch                                       # local
git branch -r                                    # remote
git branch -a                                    # all

# Create branch
git branch feature/my-feature

# Create and switch
git checkout -b feature/my-feature
git switch -c feature/my-feature                 # modern syntax

# Switch branch
git checkout main
git switch main                                  # modern syntax

# Rename branch
git branch -m old-name new-name

# Delete branch
git branch -d feature/done                       # safe delete (merged only)
git branch -D feature/done                       # force delete

# Delete remote branch
git push origin --delete feature/done

# Track remote branch
git checkout -b feature/x origin/feature/x
git checkout --track origin/feature/x            # same thing
```

---

## Staging & Committing

```bash
# Stage everything
git add .

# Stage specific file
git add src/app.py

# Stage specific lines (interactive)
git add -p src/app.py

# Selective staging (interactive)
git add -i

# Commit
git commit -m "feat: add login endpoint"

# Stage + commit tracked files (skip git add for modified files)
git commit -am "fix: correct typo"

# Amend last commit (before push)
git commit --amend -m "corrected message"
git commit --amend --no-edit                     # keep message, add staged changes

# Conventional commit format (use this)
# feat:     new feature
# fix:      bug fix
# docs:     documentation only
# style:    formatting, no logic change
# refactor: code change, not fix or feature
# test:     adding/updating tests
# chore:    build process, tooling
# ci:       CI/CD changes
```

---

## Undoing Things

```bash
# Unstage a file (keep changes)
git restore --staged src/app.py
git reset HEAD src/app.py                        # older syntax

# Discard changes in working dir (DESTRUCTIVE)
git restore src/app.py
git checkout -- src/app.py                       # older syntax

# Undo last commit, keep changes staged
git reset --soft HEAD~1

# Undo last commit, keep changes unstaged
git reset --mixed HEAD~1

# Undo last commit, discard changes (DESTRUCTIVE)
git reset --hard HEAD~1

# Revert a commit (safe — creates new commit)
git revert abc1234
git revert HEAD                                  # revert last commit

# Reset to match remote (DESTRUCTIVE — loses local changes)
git fetch origin
git reset --hard origin/main
```

---

## Rebase Workflow

> Use this instead of merge to keep history linear and clean.

```bash
# Basic rebase onto main
git checkout feature/my-feature
git rebase main

# Interactive rebase — rewrite last N commits
git rebase -i HEAD~3

# Interactive rebase options (in editor):
# pick   = keep commit as-is
# reword = keep commit, edit message
# edit   = pause to amend
# squash = melt into previous commit (keeps both messages)
# fixup  = melt into previous commit (discards this message)
# drop   = remove commit entirely

# Squash all feature commits into one before merge
git rebase -i main

# If conflicts during rebase
git status                                       # see conflicted files
# fix conflicts manually, then:
git add conflicted-file.py
git rebase --continue
# or abort entirely
git rebase --abort

# Push after rebase (force push — only on your own branch)
git push --force-with-lease origin feature/my-feature
# --force-with-lease is safer than --force (won't overwrite others' pushes)
```

---

## Remote & GitHub

```bash
# View remotes
git remote -v

# Add remote
git remote add origin https://github.com/user/repo.git
git remote add upstream https://github.com/original/repo.git

# Change remote URL
git remote set-url origin git@github.com:user/repo.git

# Remove remote
git remote remove origin

# Fetch all remotes (no merge)
git fetch --all

# Push branch and set upstream
git push -u origin feature/my-feature

# Push all branches
git push --all origin

# Pull from upstream (when forked)
git fetch upstream
git rebase upstream/main

# GitHub: create PR from CLI (gh CLI required)
gh pr create --title "feat: add feature" --body "Description"
gh pr create --base main --head feature/my-feature
```

---

## Stashing

```bash
# Stash current changes
git stash
git stash push -m "WIP: half-done login"        # with message

# Stash including untracked files
git stash -u

# List stashes
git stash list

# Apply latest stash (keeps it in stash list)
git stash apply

# Apply specific stash
git stash apply stash@{2}

# Pop latest stash (apply + remove from list)
git stash pop

# Drop a stash
git stash drop stash@{0}

# Clear all stashes
git stash clear
```

---

## Logs & Inspection

```bash
# Basic log
git log
git log --oneline                                # compact
git log --oneline --graph --all                  # visual branch graph
git log --oneline -10                            # last 10 commits

# Log with author/date
git log --pretty=format:"%h %an %ar %s"

# Log for specific file
git log --follow src/app.py

# Who changed what line (blame)
git blame src/app.py
git blame -L 10,20 src/app.py                   # specific lines

# Show a specific commit
git show abc1234
git show HEAD                                    # last commit

# Find commit by message
git log --grep="fix login"

# Find when a bug was introduced
git bisect start
git bisect bad                                   # current is broken
git bisect good v1.0                             # last known good
# git will checkout midpoints — test and mark:
git bisect good
git bisect bad
git bisect reset                                 # when done

# See file at a previous commit
git show HEAD~2:src/app.py
```

---

## Tags

```bash
# List tags
git tag

# Create annotated tag (use for releases)
git tag -a v1.0.0 -m "Release version 1.0.0"

# Create lightweight tag
git tag v1.0.0

# Tag a specific commit
git tag -a v1.0.0 abc1234 -m "Release"

# Push a tag
git push origin v1.0.0

# Push all tags
git push origin --tags

# Delete tag
git tag -d v1.0.0
git push origin --delete v1.0.0                 # remote
```

---

## GitHub CLI (`gh`)

```bash
# Install
# https://cli.github.com

# Auth
gh auth login

# Repo
gh repo create my-repo --private
gh repo clone user/repo
gh repo view

# Pull Requests
gh pr create
gh pr list
gh pr checkout 42
gh pr merge 42 --squash
gh pr close 42

# Issues
gh issue create --title "Bug: login fails" --body "Steps..."
gh issue list
gh issue close 42

# GitHub Actions
gh workflow list
gh workflow run deploy.yml
gh run list
gh run view 123456

# Releases
gh release create v1.0.0 --title "v1.0.0" --notes "Changelog..."
gh release list
```

---

## .gitignore Patterns

```gitignore
# Python
__pycache__/
*.pyc
*.pyo
*.pyd
.Python
*.egg-info/
dist/
build/
.venv/
venv/
env/
.env
.env.*
!.env.example

# Node.js
node_modules/
dist/
.next/
.nuxt/
*.log
npm-debug.log*

# Docker
.docker/

# OS
.DS_Store
Thumbs.db
*.swp
*.swo

# IDE
.vscode/
.idea/
*.iml

# Secrets (always)
*.pem
*.key
*.p12
secrets/
credentials/
```

---

## Troubleshooting

### Accidentally committed to main

```bash
git branch feature/oops              # save work in new branch
git reset --hard HEAD~1              # remove commit from main
git checkout feature/oops            # go to your branch
```

### Accidentally committed a secret

```bash
# Remove from history (rewrites commits — coordinate with team)
git filter-branch --force --index-filter \
  "git rm --cached --ignore-unmatch path/to/secret.env" \
  --prune-empty --tag-name-filter cat -- --all

# Simpler: use BFG Repo Cleaner
# https://rtyley.github.io/bfg-repo-cleaner/
# Then force push and rotate the secret immediately
git push --force --all
```

### Merge conflict resolution steps

```bash
git status                           # see conflicted files
# Open each file — look for <<<<<<< HEAD markers
# Edit to keep what you want
git add resolved-file.py
git merge --continue
# or if rebasing:
git rebase --continue
```

### Detached HEAD state

```bash
# You're on a commit, not a branch
git checkout -b new-branch-name      # save your work
# or discard and go back
git checkout main
```

### Recover deleted branch

```bash
git reflog                           # find the commit hash
git checkout -b recovered-branch abc1234
```

### Reset a single file to match remote

```bash
git fetch origin
git checkout origin/main -- src/app.py
```

### See what would be pushed

```bash
git log origin/main..HEAD --oneline
```

---

_Next file: `gitlab-cicd.md`_
