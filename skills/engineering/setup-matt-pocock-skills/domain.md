# Domain docs

Paths below are relative to the repository root.

- Layout: single-context.
- Glossary: `docs-ai/GLOSSARY.md`.
- Glossary map, if multiple contexts are introduced: `docs-ai/GLOSSARY-MAP.md`.
- ADR directory: `docs-ai/adr/`.
- Other AI working notes: `docs-ai/notes/`.

Read the glossary, or the relevant context links in the glossary map, before exploring the domain. Read ADRs relevant to the area being changed. Missing files are normal; proceed silently and create them lazily when a term or decision is resolved.

Use the glossary's canonical terms in specs, tickets, tests, and explanations. Flag a proposed decision that conflicts with an existing ADR instead of silently superseding it. Glossary maps use links relative to their own directory; new per-context documents default to `docs-ai/contexts/<context>/GLOSSARY.md` and `docs-ai/contexts/<context>/adr/`.
