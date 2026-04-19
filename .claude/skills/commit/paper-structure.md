# ABNT Paper Structure — Section Order and Anchors

This file defines the canonical ABNT section order and the anchor comments used in `build/paper.md`
for the `/commit` skill to locate and insert each section correctly.

## Section Order (ABNT NBR 14724)

| Position | Segment key | Anchor comment in paper.md | Heading |
|---|---|---|---|
| 1 | abstract | `<!-- SECTION:abstract -->` | RESUMO |
| 2 | introduction | `<!-- SECTION:introduction -->` | 1 INTRODUÇÃO |
| 3 | literature-review | `<!-- SECTION:literature-review -->` | 2 REVISÃO TEÓRICO-EMPÍRICA |
| 4 | methodology | `<!-- SECTION:methodology -->` | 3 MATERIAIS E MÉTODOS |
| 5 | results | `<!-- SECTION:results -->` | 4 RESULTADOS E DISCUSSÃO |
| 6 | conclusion | `<!-- SECTION:conclusion -->` | 5 CONSIDERAÇÕES FINAIS |
| 7 | references | `<!-- SECTION:references -->` | REFERÊNCIAS |

## Anchor Format

Each section in `build/paper.md` is delimited by a pair of anchor comments:

```
<!-- SECTION:<segment> -->
<content>
<!-- /SECTION:<segment> -->
```

When a section has not yet been committed, its anchor pair contains only a placeholder:

```
<!-- SECTION:introduction -->
<!-- PENDING -->
<!-- /SECTION:introduction -->
```

## Initial Skeleton

When `build/paper.md` does not exist yet, the `/commit` skill creates it with this skeleton:

```markdown
<!-- SECTION:abstract -->
<!-- PENDING -->
<!-- /SECTION:abstract -->

<!-- SECTION:introduction -->
<!-- PENDING -->
<!-- /SECTION:introduction -->

<!-- SECTION:literature-review -->
<!-- PENDING -->
<!-- /SECTION:literature-review -->

<!-- SECTION:methodology -->
<!-- PENDING -->
<!-- /SECTION:methodology -->

<!-- SECTION:results -->
<!-- PENDING -->
<!-- /SECTION:results -->

<!-- SECTION:conclusion -->
<!-- PENDING -->
<!-- /SECTION:conclusion -->

<!-- SECTION:references -->
<!-- PENDING -->
<!-- /SECTION:references -->
```
