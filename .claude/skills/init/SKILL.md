---
name: init
description: Initialize the research context for a new academic project. Asks the researcher for topic, research area, problem, approach, and optional institutional formatting reference, then writes Research Context and Formatting Reference sections to CLAUDE.md. Run once before starting.
argument-hint: (no arguments needed)
allowed-tools: Read Edit Write WebFetch
---

You are initializing a new academic research project. Your job is to collect key information from the researcher through a guided conversation, then save a Research Context section — and optionally a Formatting Reference section — to `CLAUDE.md`.

---

## Step 1 — Welcome

Greet the researcher briefly. Explain that you will ask a few questions (2 mandatory, 2 optional, and 1 about formatting) to set up the project context. This context will be saved to `CLAUDE.md` and will guide every future session.

---

## Step 2 — Collect: Research Topic (mandatory)

Ask: **"Qual é o tema da sua pesquisa?"**

- Wait for a response.
- If the researcher says they do not know, are unsure, or asks for help, guide them with research methodology:
  - Explain that a good research topic is **specific and delimited** — not "tecnologia", but "uso de inteligência artificial no diagnóstico de doenças raras em crianças".
  - Ask them:
    - "Qual é o seu curso ou área de formação?"
    - "Que problema ou situação chamou sua atenção recentemente?"
    - "O que você já leu ou estudou que achou interessante?"
  - Use their answers to suggest 2–3 possible topic framings.
  - Let them choose or refine.
- Do not proceed until a topic is provided.

---

## Step 3 — Collect: Research Area (mandatory)

Ask: **"Qual é a área de pesquisa? (ex: Ciências da Computação, Administração, Direito, Engenharia Civil, Psicologia, Medicina, Educação...)"**

- Wait for a response.
- If the researcher is unsure, explain:
  - The research area is the **broad academic discipline**, not the topic itself.
  - Examples: Ciências da Saúde, Ciências Sociais Aplicadas, Ciências Humanas, Engenharias, Ciências Exatas e da Terra, Linguística e Artes, Ciências Biológicas.
  - Help them identify the area based on their topic and course.
- Do not proceed until an area is provided.

---

## Step 4 — Collect: Problem(s) to Solve (optional)

Ask: **"Qual ou quais problemas você pretende resolver? (pode deixar em branco ou responder 'não sei' se ainda não souber)"**

- Wait for a response.
- If the researcher says they do not know or asks for help, guide them:
  - A research problem is a **gap, contradiction, or deficiency** in current knowledge or practice. It answers: "O que ainda não se sabe? O que está acontecendo de errado? O que precisa melhorar?"
  - Give a concrete example tailored to their topic (e.g., if the topic is IA in healthcare: "Muitos sistemas de triagem hospitalar ainda dependem de avaliação manual, o que gera atrasos e inconsistências — o problema é: como a IA pode reduzir erros e tempo de espera?").
  - Offer them 1–2 examples of problems that fit their topic.
- Accept if left blank or skipped — store as "Não definido ainda".

---

## Step 5 — Collect: Proposed Approach (optional)

Ask: **"Como você pretende resolver esse(s) problema(s)? (pode deixar em branco ou responder 'não sei' se ainda não souber)"**

- Wait for a response.
- If the researcher is unsure or asks for help, suggest approaches common to their research area and explain each briefly:
  - **Revisão bibliográfica/sistemática** — levantamento e análise crítica da literatura existente.
  - **Estudo de caso** — análise aprofundada de um caso específico (empresa, sistema, evento).
  - **Pesquisa de campo / survey** — coleta de dados primários via questionários ou entrevistas.
  - **Experimento / prova de conceito** — construção e teste de um sistema, modelo ou protótipo.
  - **Análise documental** — exame de documentos, legislação, relatórios, dados secondários.
  - Tailor the suggestion list to their area (e.g., for Engenharia lean toward experiment/PoC; for Ciências Humanas lean toward bibliographic or field research).
- Accept if left blank or skipped — store as "Não definida ainda".

---

## Step 6 — Collect: Institutional Formatting Reference (optional)

Ask:

> "Sua instituição tem um guia de formatação próprio para o TCC?
> - Cole uma **URL pública** do documento (ex: link do manual da universidade)
> - Ou informe o nome de um **arquivo em `docs/`** (ex: `docs/normas-ufsc.pdf`)
> - Ou pressione **Enter** para usar as normas ABNT genéricas do framework"

Wait for a response and handle each case:

### If a URL is provided:
1. Use WebFetch to retrieve the document.
2. Extract the following formatting rules (where present):
   - Page margins (top, bottom, left, right)
   - Font family and size
   - Line spacing (body text, quotes, references, captions)
   - Paragraph indentation
   - Section numbering style and maximum depth
   - Pagination rules (start page, position)
   - Citation style (direct/indirect, authorship format)
   - Reference list rules (ordering, spacing, punctuation)
   - Any institution-specific additions or deviations from ABNT
3. Compare extracted rules against the generic ABNT rules already in `CLAUDE.md`.
4. Identify **divergences** (institution overrides the standard) and **confirmations** (matches the standard).
5. Store the result for Step 8.

### If a file in `docs/` is provided:
1. Read the file using the Read tool.
2. Apply the same extraction and comparison logic above.
3. Store the result for Step 8.

### If left blank or skipped:
- Store reference source as `null`.
- Skip Step 8 entirely.

---

## Step 7 — Write Research Context to CLAUDE.md

1. Read `CLAUDE.md`.
2. Check if a `## Research Context` section already exists (search for the exact heading).
3. Build the section content using the collected answers:

```
---

## Research Context

> Esta seção foi gerada pelo `/init`. Para atualizar, execute `/init` novamente.

- **Tema:** <topic>
- **Área:** <research area>
- **Problema(s):** <problems, or "Não definido ainda">
- **Abordagem:** <approach, or "Não definida ainda">
```

4. If the section **does not exist** → append the section to the end of `CLAUDE.md`.
5. If the section **already exists** → replace everything from `## Research Context` to the end of that block with the new content.

---

## Step 8 — Write Formatting Reference to CLAUDE.md (only if reference was provided)

Skip this step entirely if no reference was provided in Step 6.

1. Read `CLAUDE.md` to find any existing `## Formatting Reference` section.
2. Build the section using the extraction results from Step 6:

```markdown
## Formatting Reference

> Generated by `/init` on <YYYY-MM-DD>. To update, run `/format`.
> Source: <URL or filename>

### Institution-specific overrides (diverge from generic ABNT)
- <rule>: <institution value> *(ABNT default: <default value>)*
- ...

### Confirmed rules (match ABNT standard)
- <rule>: <value>
- ...
```

3. If the section **does not exist** → append it immediately after `## Research Context` in `CLAUDE.md`.
4. If the section **already exists** → replace it with the new content.
5. If any extracted rules affect section writing (citations, quotation blocks, reference formatting), update the corresponding rule file(s) in `.claude/skills/conclusion-paper-writer/rules/` by appending an `## Institution-Specific Overrides` block at the end of the affected file(s). Do not remove or alter existing content — only append.

---

## Step 9 — Confirm and suggest next step

- Show the researcher a summary of what was saved (research context fields + whether a formatting reference was found and applied).
- If a formatting reference was applied, list the key divergences found.
- Tell them: "O contexto de pesquisa foi salvo em `CLAUDE.md`. Agora você pode rodar `/research <seu tema>` para iniciar a pesquisa."
- If no reference was provided, add: "Se quiser ajustar a formatação a qualquer momento, rode `/format`."
