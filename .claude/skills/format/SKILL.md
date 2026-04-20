---
name: format
description: Refine the formatting rules of the TCC at any point in the process. Accepts a public URL, a file in docs/, or a plain-language adjustment. Updates CLAUDE.md and the conclusion-paper-writer rule files automatically. Run after /init whenever the researcher needs to add, correct, or override a formatting rule.
argument-hint: [URL | docs/<file> | "plain-language adjustment"]
allowed-tools: Read Edit WebFetch
---

You are a formatting assistant for an academic TCC project. Your job is to update the formatting rules stored in `CLAUDE.md` and in `.claude/skills/conclusion-paper-writer/rules/` based on input from the researcher.

Always show proposed changes clearly before applying them. Never apply changes without researcher confirmation.

---

## Step 1 — Determine input mode

Check whether the researcher provided an argument:

### No argument → Interactive mode
1. Read the `## Formatting Reference` section from `CLAUDE.md`.
2. If the section exists, display the current rules to the researcher in a readable format.
3. If the section does not exist, inform: "Nenhuma referência de formatação foi configurada ainda. Você pode fornecer uma URL, um arquivo em `docs/`, ou descrever o ajuste desejado."
4. Ask: "O que deseja ajustar? Cole uma URL, o nome de um arquivo em `docs/`, ou descreva a mudança (ex: 'fonte Times New Roman', 'margem esquerda 4 cm')."
5. Wait for input, then proceed to the appropriate case below.

### URL argument → proceed to Step 2A
### `docs/<file>` argument → proceed to Step 2B
### Plain-language text → proceed to Step 2C

---

## Step 2A — Process URL

1. Use WebFetch to retrieve the document at the provided URL.
2. Extract all formatting rules present in the document:
   - Page margins (top, bottom, left, right)
   - Font family and size
   - Line spacing (body text, quotes, references, captions)
   - Paragraph indentation
   - Section numbering style and maximum depth
   - Pagination rules (start page, position)
   - Citation style (direct/indirect, authorship format)
   - Reference list rules (ordering, spacing, punctuation)
   - Any institution-specific additions or deviations from ABNT
3. Read the current `## Formatting Reference` section from `CLAUDE.md` (if any).
4. Compare new rules against current rules.
5. Proceed to Step 3.

---

## Step 2B — Process file in docs/

1. Read the file from `docs/` using the Read tool.
2. Apply the same extraction logic as Step 2A.
3. Read the current `## Formatting Reference` section from `CLAUDE.md` (if any).
4. Compare new rules against current rules.
5. Proceed to Step 3.

---

## Step 2C — Process plain-language adjustment

1. Parse the researcher's description to identify the specific rule being changed.
   - Examples:
     - "fonte Times New Roman" → font family rule
     - "margem esquerda 4 cm" → left margin rule
     - "espaçamento simples no corpo" → body line spacing rule
     - "citações com nota de rodapé" → citation style rule
2. Read the current `## Formatting Reference` section from `CLAUDE.md` (if any) to get the existing value for that rule.
3. Build a minimal change targeting only the affected rule.
4. Proceed to Step 3.

---

## Step 3 — Show proposed changes and ask for confirmation

Present a clear diff of proposed changes:

```
Mudanças propostas na formatação:

  REGRA              ATUAL                    NOVO
  ─────────────────────────────────────────────────────
  Fonte              Arial 12pt               Times New Roman 12pt
  Margem esquerda    3 cm                     4 cm
  ...

Deseja aplicar essas alterações? (sim / não / ajustar)
```

- If the researcher says **não** or wants to adjust, ask what to change and loop back.
- If the researcher says **sim**, proceed to Step 4.

---

## Step 4 — Apply changes

### 4A — Update CLAUDE.md

1. Read `CLAUDE.md`.
2. Locate the `## Formatting Reference` section.
3. If it exists → update only the changed rules within it, preserving the structure:

```markdown
## Formatting Reference

> Updated by `/format` on <YYYY-MM-DD>. Source: <URL, filename, or "manual adjustment">

### Institution-specific overrides (diverge from generic ABNT)
- <rule>: <new value> *(ABNT default: <default value>)*
- ...

### Confirmed rules (match ABNT standard)
- <rule>: <value>
- ...
```

4. If the section does not exist → create it at the end of `CLAUDE.md` with only the rules that were explicitly changed.

### 4B — Update affected rule files

For each rule that was changed, identify which section rule files are affected:

| Changed rule | Affected rule files |
|---|---|
| Citation style / authorship format | All rule files (all sections cite sources) |
| Long quotation block format | `abstract.md`, `introduction.md`, `theorical-empirical-revision.md`, `methodology.md`, `results.md`, `conclusion-recomendation.md` |
| Reference list format | `references.md` |
| Abstract word count or structure | `abstract.md` |
| Section numbering | `introduction.md` |

For each affected rule file:
1. Read the file.
2. Check if an `## Institution-Specific Overrides` block already exists at the bottom.
3. If it exists → update the relevant entry within it.
4. If it does not exist → append the block:

```markdown

---

## Institution-Specific Overrides

> Applied by `/format` on <YYYY-MM-DD>.

- <rule>: <new value> *(overrides ABNT default: <default value>)*
```

Do not modify any existing content above this block.

---

## Step 5 — Confirm

Summarize what was updated:

```
Formatação atualizada com sucesso.

  Arquivos modificados:
  - CLAUDE.md (seção ## Formatting Reference)
  - .claude/skills/conclusion-paper-writer/rules/references.md
  - ...

As próximas seções escritas com /write usarão as novas regras.
Se precisar ajustar novamente, rode /format.
```
