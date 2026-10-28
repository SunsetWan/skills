---
name: project-skill-config
description: Resolve project configuration before reading or writing engineering specs, tickets, domain glossaries, ADRs, or AI working notes. Use when another skill needs the issue tracker, triage labels, or document paths.
---

# Project skill configuration

Resolve paths before the calling skill reads or writes project documents. This skill reads configuration; it does not initialize a project or migrate its files.

## Resolve configuration

1. Find the target repository root, including when invoked from a subdirectory. In a submodule, use that submodule's root. Without a repository, use the user's working directory.
2. Follow explicit user destinations and applicable project instructions first. A project instruction may name a different configuration directory. Otherwise, read `docs-ai/agents/issue-tracker.md`, `domain.md`, and `triage-labels.md` when present. For each missing configuration file, read its legacy `docs/agents/` counterpart if present. New configuration wins over the corresponding legacy file; do not combine conflicting values. Report a material conflict and the selected source.
3. Resolve document paths from those configuration files. Paths stated as repository-relative resolve from the root; links inside a glossary map resolve from the map's directory. A configured missing destination is still the destination: create it lazily when the calling task needs it, rather than falling back to a different store.
4. For fields not configured, discover existing domain documents: `GLOSSARY-MAP.md`, `GLOSSARY.md`, then legacy `CONTEXT-MAP.md` / `CONTEXT.md` at the root. Follow a map to its relevant contexts. Use existing `docs/adr/` and context-scoped ADR locations. Preserve their paths and names. For unconfigured local tasks, retain an existing `.scratch/` convention.
5. For fields still unresolved, use the new-project defaults below. Existing `docs-ai/GLOSSARY-MAP.md` supplies its context links. Missing domain documents are normal: continue silently and create them only when there is content to write.

| Field | New-project default, relative to root |
| --- | --- |
| Configuration directory | `docs-ai/agents/` |
| Local task root | `docs-ai/tasks/` |
| Glossary | `docs-ai/GLOSSARY.md` |
| Glossary map | `docs-ai/GLOSSARY-MAP.md` |
| ADR directory | `docs-ai/adr/` |
| Other AI working notes | `docs-ai/notes/` |

Return the selected configuration sources, tracker (or unconfigured), triage mapping (or unconfigured), and resolved paths to the calling skill. Interpret its shorthand `GLOSSARY.md`, `GLOSSARY-MAP.md`, ADR directory, and local task root as these resolved destinations for both reads and writes. Pass this context to any subagent that works with those documents. Passive vocabulary reading does not require active domain modeling.

## Publication and compatibility

- Tracker selection is independent of document storage. Read the configured GitHub, GitLab, local, or custom workflow. Never infer permission to publish issues from a Git remote or from an ignored directory. When a calling workflow requires a tracker or label mapping and none is configured, tell the user to run `/setup-matt-pocock-skills`; never invoke that user-only skill automatically.
- Honor an explicit user deliverable path. Formal README files, public specifications, source files, and a deliberately selected teaching workspace retain their intended locations. OS-temporary handoffs retain their temporary-directory convention. These defaults govern AI working documents, not every Markdown file.
- Keep existing configuration and documents in place. Migration happens only through an explicitly requested setup run with an approved source-to-destination plan. If old and new documents coexist, use the configured destination; do not merge or delete the others.
- In a Git repository, before creating a default local document under `docs-ai/`, verify it is ignored with `git check-ignore --no-index` and check `git ls-files -- docs-ai`. If needed, add `/docs-ai/` to the owning repository's `.gitignore` as part of the authorized write, preserving its other entries, then verify again. If existing exceptions still expose the destination, resolve that before writing. Already tracked files remain tracked despite ignore rules: report them and obtain migration/untracking authorization before treating them as local-only. Never force-add local documents or rewrite history as part of setup.
