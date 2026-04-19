---
name: approve
description: Mark a draft in write/ as approved after human review. Changes status from pending to approved. Only approved files can be committed to the final paper with /commit.
argument-hint: [write-file]
allowed-tools: Read Edit
---

Approve the draft file: **$ARGUMENTS**

Follow these steps:

1. **Read the file** at `$ARGUMENTS`

2. **Check the current status** in the frontmatter:
   - If `status: approved` → inform the student: "This file is already approved."
   - If `status: committed` → inform the student: "This file is already committed to the paper."
   - If `status: pending` → proceed to step 3

3. **Update the status**: change `status: pending` to `status: approved` in the frontmatter

4. **Confirm** to the student:
   > "`$ARGUMENTS` approved.
   > Run `/commit $ARGUMENTS` to integrate this section into the paper."
