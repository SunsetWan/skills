---
name: setup-matt-pocock-skills
description: "Configure this repo's issue tracker, triage labels, and local AI document paths. Run before first use of the engineering workflow."
disable-model-invocation: true
---

# Setup Matt Pocock's Skills

This is a prompt-driven setup, not a deterministic installer. Reuse choices already approved in this conversation. Present unresolved choices and a concrete draft before writing.

## 1. Explore

Call the Skill tool with "project-skill-config". If the harness has no Skill tool, load that installed skill's `SKILL.md` through its skill discovery mechanism. It owns configuration precedence, legacy discovery, and local-document protection.

Inspect the Git remote, applicable project instructions, resolved configuration, existing Glossary/Context maps and ADRs, `.scratch/`, and `docs-ai/`. Check tracked files and ignore rules. Check whether `triage` is installed. Look for real multi-context signals, such as a workspace with multiple populated packages; a standalone test-tools package is not enough.

Existing configuration remains authoritative until the user approves changing it. If a migration is requested, list each old and new path, link updates, tracking changes, and any conflicts. Preserve unrelated content and history. Do not automatically rename legacy Context files or move old documents.

## 2. Settle configuration

Ask only unresolved choices, in this order:

- **Tracker**: offer the actual GitHub or GitLab remote when present, local Markdown, or a custom workflow. A remote is a recommendation, not permission to publish. Local Markdown uses the resolved task root, default `docs-ai/tasks/`. Keep the remote templates' PR request-surface flag off unless requested.
- **Triage labels**, only if `triage` is installed: recommend the five canonical names in [triage-labels.md](./triage-labels.md). Retain any existing mapping unless a change is approved.
- **Domain layout**: use a single context by default. Only offer multiple contexts when the repository needs them. New context documents live under `docs-ai/contexts/<context>/`, with links from the configured glossary map; retain an existing layout unless migration is approved.

New configuration lives in `docs-ai/agents/`. An explicit project override may choose another configuration directory. References in generated configuration must use the selected paths, not unresolved placeholders or seed defaults.

## 3. Draft and write

Show the proposed `issue-tracker.md`, `domain.md`, and, when applicable, `triage-labels.md`, plus the ignore-rule change or explicit migration plan. Existing approval of these exact choices is sufficient; do not ask the same questions again.

Use these seed templates and replace their paths for the resolved layout:

- [issue-tracker-local.md](./issue-tracker-local.md)
- [issue-tracker-github.md](./issue-tracker-github.md)
- [issue-tracker-gitlab.md](./issue-tracker-gitlab.md)
- [domain.md](./domain.md)
- [triage-labels.md](./triage-labels.md)

For a custom tracker, record the user's workflow as prose. For a local tracker, all issue, comment, status, and wayfinding operations remain local. For a remote tracker, create missing configured labels only when that remote setup is authorized.

Apply the local-document protection in `project-skill-config` before writing. Update existing configuration in place, preserving user customizations. Create domain documents and task files lazily, not as empty scaffolding. Consumers discover configuration through the shared reader, so setup does not create or edit root `AGENTS.md` or `CLAUDE.md` navigation blocks.

## 4. Verify and report

Verify the written paths, ignore behavior, and selected tracker. Check that local-only documents are not tracked or staged. Report which configuration files were written, any explicitly approved migration, and that remote operations remain governed by tracker selection and task authorization. Users may edit these files directly or rerun setup to change their configuration.
