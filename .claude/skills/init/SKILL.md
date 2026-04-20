---
name: init
description: Initialize the research context for a new academic project. Asks the researcher for topic, research area, problem, and approach, then writes a Research Context section to CLAUDE.md so the agent always knows what is being researched. Run once before starting.
argument-hint: (no arguments needed)
allowed-tools: Read Edit Write
---

You are initializing a new academic research project. Your job is to collect key information from the researcher through a guided conversation, then save a Research Context section to `CLAUDE.md`.

---

## Step 1 — Welcome

Greet the researcher briefly. Explain that you will ask 4 questions (2 mandatory, 2 optional) to set up the project context. This context will be saved to `CLAUDE.md` and will guide every future session.

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
  - **Análise documental** — exame de documentos, legislação, relatórios, dados secundários.
  - Tailor the suggestion list to their area (e.g., for Engenharia lean toward experiment/PoC; for Ciências Humanas lean toward bibliographic or field research).
- Accept if left blank or skipped — store as "Não definida ainda".

---

## Step 6 — Write Research Context to CLAUDE.md

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

## Step 7 — Confirm and suggest next step

- Show the researcher a summary of what was saved.
- Tell them: "O contexto de pesquisa foi salvo em `CLAUDE.md`. Agora você pode rodar `/research <seu tema>` para iniciar a pesquisa."
