---
name: publish
description: Generate a commit message from pending git changes and push to the configured remote repository. Requires git to be initialized and a remote configured.
allowed-tools: Bash(git *)
---

Publish the current TCC progress to the remote repository.

Follow these steps:

## Step 1 — Verify git is initialized

Run `git status`.
- If the command fails (not a git repo): stop and instruct the student:
  > "Git is not initialized. Run:
  > ```
  > git init
  > git remote add origin <your-repo-url>
  > ```
  > Then run `/publish` again."

## Step 2 — Verify a remote is configured

Run `git remote -v`.
- If no remote is listed: stop and instruct the student:
  > "No remote configured. Run:
  > ```
  > git remote add origin <your-repo-url>
  > ```
  > Then run `/publish` again."

## Step 3 — Summarize changes

Run:
```bash
git diff --stat HEAD
git diff --name-only HEAD
git status --short
```

Identify which sections were added, modified, or committed based on the changed file paths:
- Files in `research/` → research activity
- Files in `write/` → section drafts
- Files in `build/` → paper consolidation
- Files in `dist/` → releases

## Step 4 — Generate commit message

Based on the changed files, write a concise, descriptive commit message that summarizes what was done. Examples:
- "Add introduction draft; approve methodology"
- "Commit results section to paper; regenerate DOCX"
- "Research inteligência artificial na educação"

## Step 5 — Stage and commit

```bash
git add research/ write/ build/ dist/ README.md CLAUDE.md
git commit -m "<generated message>"
```

## Step 6 — Push

```bash
git push
```

If the push is rejected (e.g., diverged history), report the error and suggest `git pull --rebase` before pushing again.

## Step 7 — Confirm

Report the commit hash and a summary of what was pushed.
