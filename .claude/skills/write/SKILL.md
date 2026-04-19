---
name: write
description: Draft a TCC paper section based on a research file. Orchestrates the conclusion-paper-writer skill to apply ABNT section rules. Saves the draft to write/<segment>-<date>.md with status pending. Valid segments: abstract, introduction, literature-review, methodology, results, conclusion, references.
argument-hint: [research-file] [segment]
allowed-tools: Read Write Bash
---

Draft a TCC section using the following inputs:
- Research file: **$0**
- Segment: **$1**

Follow these steps exactly:

## Step 1 — Validate inputs

Verify:
- `$0` file exists; if not, stop and tell the student the path was not found
- `$1` is one of: `abstract`, `introduction`, `literature-review`, `methodology`, `results`, `conclusion`, `references`; if not, list the valid options and stop

## Step 2 — Load the ABNT rules for the segment

Read the matching rules file from `.claude/skills/conclusion-paper-writer/rules/`:

| Segment | Rules file |
|---|---|
| abstract | abstract.md |
| introduction | introduction.md |
| literature-review | theorical-empirical-revision.md |
| methodology | methodology.md |
| results | results.md |
| conclusion | conclusion-recomendation.md |
| references | references.md |

## Step 3 — Read the research file

Read `$0` in full. Extract:
- Research Results section
- Conclusion section
- Cited Sources

## Step 4 — Draft the section

Using the ABNT rules loaded in Step 2 and the research content from Step 3, draft the section following the `conclusion-paper-writer` skill guidelines:
- Never fabricate data, results, or scientific claims — only use content from the research file
- Apply all ABNT norms for the chosen segment (structure, tense, person, spacing, citation format)
- Citations: use ABNT NBR 10520 format as defined in CLAUDE.md
- Language: write in the same language the research file is written in (default: Portuguese BR)

## Step 5 — Save the draft

Determine today's date in YYYY-MM-DD format.
Save to `write/<segment>-<YYYY-MM-DD>.md` using this frontmatter:

```
---
segment: <segment>
research-source: $0
status: pending
date: <YYYY-MM-DD>
---
```

Followed immediately by the drafted content.

## Step 6 — Present to student

Show the draft inline and provide a brief ABNT compliance checklist for the student to verify before approving:
- [ ] Structure matches the required elements for this section
- [ ] Verb tense is correct for the section type
- [ ] All in-text citations follow ABNT NBR 10520
- [ ] No fabricated data or unsupported claims
- [ ] Formatting norms (spacing, indentation) are indicated in the file

Remind the student: "Review the draft, then run `/approve write/<segment>-<date>.md` when satisfied."
