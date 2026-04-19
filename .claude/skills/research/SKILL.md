---
name: research
description: Start an agentic research session for the TCC. Searches and summarizes findings from the web and from files in docs/. Saves a structured research file in research/. Use when the student wants to investigate a topic for the conclusion paper.
argument-hint: [topic or research question]
allowed-tools: WebSearch WebFetch Read Write Bash
---

Research the following topic for the TCC: **$ARGUMENTS**

Follow these steps exactly:

1. **Check docs/ for primary sources**
   - List files in `docs/` (excluding `.gitkeep`)
   - If any files exist, read them and treat them as primary sources — extract relevant excerpts and page numbers

2. **Web search**
   - Search for the topic using multiple queries to cover different angles (concepts, recent studies, Brazilian/global context as applicable)
   - Fetch and read the most relevant pages

3. **Structure the research file**
   - Use the template at `.claude/skills/research/template.md` as the output format
   - Derive a URL-safe slug from the topic (lowercase, hyphens, no accents or special characters)
   - Save the file to `research/<slug>-<YYYY-MM-DD>.md` using today's date

4. **Fill the template sections**
   - `## Research Results` — factual prose summary of findings; never fabricate data or claims
   - `## Conclusion` — 3-5 sentence synthesis of what these findings mean for the TCC
   - `## Cited Sources`:
     - Web sources: `- Author (Year). *Title*. <URL>`
     - File sources: include excerpt and page number as shown in the template

5. **Report** the saved file path to the student and list a brief summary of what was found.
