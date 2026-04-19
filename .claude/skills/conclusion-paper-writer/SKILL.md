---
name: conclusion-paper-writer
description: >
  Use this skill whenever the user wants to write, review, improve, or get guidance on 
  any section of a Brazilian academic TCC (Trabalho de Conclusão de Curso) or scientific 
  paper following Brazilian ABNT norms. This includes writing or evaluating the abstract 
  (resumo), introduction, theoretical-empirical revision (revisão teórico-empírica), 
  methodology (metodologia), results/data analysis (resultados), conclusions and 
  recommendations (conclusões e recomendações), or references (referências). Trigger this 
  skill even when the user says things like "help me write my abstract", "how should I 
  structure my methodology", "review my introduction", "write my conclusion chapter", 
  "how do I format references", or "what goes in the results section". Also trigger for 
  ABNT formatting rules or academic writing in Portuguese (Brazil).
  NOTE: This skill is tailored for Brazilian academic standards (ABNT norms). It cannot 
  be fully applied to papers following other countries' formatting standards (APA, MLA, 
  Vancouver, etc.).
---

# Conclusion Paper Writer

A skill for writing, reviewing, and guiding the production of Brazilian academic TCC 
(Trabalho de Conclusão de Curso) segments, strictly following **Brazilian ABNT norms** 
(NBR 6023, NBR 10520, NBR 6024, etc.).

> **Scope notice:** This skill is designed for Brazilian academic papers under ABNT 
> standards. It is **not** fully applicable to papers following international formatting 
> standards (APA, MLA, Vancouver, Chicago, etc.).

## Overview

A complete scientific article is composed of the following segments.
Each segment has its own rules file. **Always read the relevant rules file before writing or 
reviewing that segment.**

| Segment | When to Use | Rules File |
|---|---|---|
| Abstract (Resumo) | Writing/reviewing the summary of the paper | `rules/abstract.md` |
| Introduction (Introdução) | Writing/reviewing Chapter 1 | `rules/introduction.md` |
| Theoretical-Empirical Revision | Writing/reviewing Chapter 2 (literature review) | `rules/theorical-empirical-revision.md` |
| Methodology | Writing/reviewing Chapter 3 | `rules/methodology.md` |
| Results (Data Analysis) | Writing/reviewing Chapter 4 | `rules/results.md` |
| Conclusions & Recommendations | Writing/reviewing Chapter 5 | `rules/conclusion-recomendation.md` |
| References | Writing/reviewing the reference list | `rules/references.md` |

---

## How to Use This Skill

### Step 1 — Identify the Segment
Determine which paper segment the user is working on. If unclear, ask:
> "Which part of your paper are you working on? (e.g., abstract, introduction, methodology, 
> results, conclusion, or references?)"

### Step 2 — Read the Relevant Rules File
Before writing or reviewing, **always read the corresponding rules file** using the view tool.
Example: if the user wants to write their methodology, read `rules/methodology.md` first.

Multiple segments in one request? Read all relevant rule files.

### Step 3 — Gather the Necessary Context
Depending on the segment, ask for what you need:

| Segment | What You Need from the User |
|---|---|
| Abstract | Draft or full paper content (objective, method, results, conclusions) |
| Introduction | Research topic, research question, general/specific objectives, justification |
| Theoretical Revision | Specific objectives, theoretical pillars, available sources |
| Methodology | Research approach, classification, population, instruments used |
| Results | Specific objectives, collected data, theoretical framework used |
| Conclusions | Specific objectives, general objective, findings from Chapter 4 |
| References | List of works cited in the text |

### Step 4 — Write or Review Following the Rules
Apply the rules from the relevant file strictly. Do not invent rules or deviate from 
the guidelines in the rules files.

---

## Paper Structure and Alignment Principle

The paper must maintain **total internal alignment** across all sections:

```
Research Question (Introduction)
      ↓
General Objective (Introduction)
      ↓
Specific Objectives (Introduction)
      ↓
Theoretical Pillars (Chapter 2) ← must match specific objectives
      ↓
Data Collection Instrument (Chapter 3) ← built from Chapter 2 theory
      ↓
Results Sections (Chapter 4) ← one section per specific objective
      ↓
Conclusion (Chapter 5) ← answers each objective and the research question
      ↓
Abstract ← summarizes objectives, method, results, conclusions
```

**If any segment is misaligned, point it out and suggest corrections.**

---

## General Academic Writing Rules

These apply to ALL segments:

- Use **impersonal language** throughout (avoid first-person "I" or "we")
- Be **clear, concise, and objective**
- All theoretical claims must be **supported by citations** (ABNT format)
- Maintain consistent terminology across the entire paper
- Formatting: Times New Roman 12 (or Arial 12), 1.5 line spacing (body), margins: top 3cm, bottom 2cm, left 3cm, right 2cm, A4 paper (ABNT NBR 14724)
- Section titles: numbered with Arabic numerals, left-aligned, bold
  - Primary sections: TNR 14, bold
  - Secondary sections: TNR 12, bold
  - Tertiary sections: TNR 12, normal
  - Quaternary sections: TNR 12, italic

---

## Title Rule
The paper title must reflect the general objective directly.
Simply convert the initial infinitive verb to its corresponding noun form.

Example:
- General objective: "Analyze the use of security systems in Organization X"
- Title: "Analysis of the use of security systems in Organization X"

---

## Quick Reference: Segment Chaining

When helping a user write a complete paper or multiple segments, follow this suggested 
writing order to maintain alignment:
1. Define research question + objectives → Introduction
2. Identify theoretical pillars → Theoretical Revision
3. Define methods → Methodology
4. Present + analyze data → Results
5. Summarize findings → Conclusion
6. Synthesize everything → Abstract
7. List all cited sources → References
