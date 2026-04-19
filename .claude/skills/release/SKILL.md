---
name: release
description: Export the consolidated paper to a versioned PDF in dist/. Increments the release number automatically (1-release-paper.pdf, 2-release-paper.pdf, ...). Requires pandoc; falls back to .md if pandoc is not available.
allowed-tools: Bash Read Write
---

Export the consolidated paper to a versioned release in `dist/`.

Follow these steps:

## Step 1 — Verify the paper exists

Read `build/paper.md`.
- If the file does not exist: stop with "No paper found. Run `/commit` to consolidate sections into `build/paper.md` first."
- If the file exists but contains only `<!-- PENDING -->` anchors with no real content: warn the student that no sections have been committed yet, and ask for confirmation before proceeding.

## Step 2 — Determine the next version number

List all files in `dist/`:
- Find files matching the pattern `<N>-release-paper.*`
- Extract the highest `N`; next version = `N + 1`
- If no release files exist, version = 1

## Step 3 — Export to PDF

Try:
```bash
pandoc build/paper.md \
  --from markdown \
  --to pdf \
  --output dist/<N>-release-paper.pdf \
  --variable mainfont="Arial" \
  --variable fontsize=12pt \
  --variable geometry="top=3cm, bottom=2cm, left=3cm, right=2cm" \
  --variable linestretch=1.5 \
  --variable indent=true
```

**If pandoc is not installed:**
- Copy `build/paper.md` to `dist/<N>-release-paper.md`
- Inform the student: "pandoc is not installed — saved as Markdown. Install pandoc at https://pandoc.org/installing.html to generate PDF releases."

**If pandoc fails** (e.g., missing LaTeX engine for PDF):
- Try generating DOCX instead: replace `--to pdf` with `--to docx` and output `dist/<N>-release-paper.docx`
- Inform the student of the fallback and suggest installing a LaTeX distribution for PDF output

## Step 4 — Confirm

Report:
> "Release **v<N>** saved to `dist/<N>-release-paper.<ext>`."
> List all releases in `dist/` so the student can see the full history.
