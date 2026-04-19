---
name: commit
description: Consolidate an approved write/ draft into build/paper.md following ABNT section order, then regenerate build/paper.docx via pandoc. Updates the draft status to committed. Only approved files can be committed.
argument-hint: [write-file]
allowed-tools: Read Write Edit Bash
---

Commit the approved draft into the paper: **$ARGUMENTS**

Follow these steps exactly:

## Step 1 — Read and validate the draft

Read `$ARGUMENTS`. Check frontmatter:
- If `status` is `pending` → stop: "This file has not been approved yet. Run `/approve $ARGUMENTS` first."
- If `status` is `committed` → stop: "This section is already committed."
- If `status` is `approved` → proceed

Note the `segment` value from the frontmatter (e.g., `introduction`).

## Step 2 — Prepare build/paper.md

Read `.claude/skills/commit/paper-structure.md` to understand section order and anchor format.

Check if `build/paper.md` exists:
- **If it does not exist**, create it with the full ABNT skeleton (all 7 section anchor pairs with `<!-- PENDING -->` placeholders, as defined in paper-structure.md)
- **If it exists**, read it in full

## Step 3 — Insert the section content

Locate the anchor block for the draft's segment:
```
<!-- SECTION:<segment> -->
...any existing content or <!-- PENDING -->...
<!-- /SECTION:<segment> -->
```

Replace everything between the opening and closing anchor comments with the draft content (everything after the frontmatter `---` block in the write file).

Write the updated `build/paper.md`.

## Step 4 — Regenerate the DOCX

Check if pandoc is installed:
```bash
pandoc --version
```

**If pandoc is not installed:**
- Skip DOCX generation
- Inform the student:
  > "pandoc is not installed — DOCX not generated. Install pandoc at https://pandoc.org/installing.html to enable DOCX output."
- Continue to Step 5.

**If pandoc is installed**, run:
```bash
pandoc build/paper.md \
  --from markdown \
  --to docx \
  --output build/paper.docx \
  --variable mainfont="Arial" \
  --variable fontsize=12pt \
  --variable geometry="top=3cm, bottom=2cm, left=3cm, right=2cm" \
  --variable linestretch=1.5 \
  --variable indent=true
```

If the command fails, report the error and continue — the `.md` source is always updated regardless.

## Step 5 — Update the draft status

In `$ARGUMENTS`, change `status: approved` to `status: committed`.

## Step 6 — Confirm

Report to the student:
> "Section `<segment>` committed to `build/paper.md`.
> `build/paper.docx` updated (or: pandoc not available — install it to enable DOCX output).
> Draft marked as `committed`."
>
> Sections still pending: list any `<!-- PENDING -->` anchors remaining in `build/paper.md`.
