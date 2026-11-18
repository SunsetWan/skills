---
name: pr
description: "Use when writing a PR body."
metadata:
  credits:
    skill: show-me
    author: Dex Horthy
    organisation: Humanlayer
    url: "https://github.com/humanlayer/skills/blob/main/plugins/show-me/skills/show-me/SKILL.md"
---

Call the Skill tool with "project-skill-config" before reading or writing project documents. If this harness has no Skill tool, load that installed skill's `SKILL.md` through skill discovery. Use its resolved tracker, labels, and document paths throughout this skill and pass them to subagents.

Write a single `## Summary` section. Use the project's domain language.

Default to one or two sentences. Lead with what changed and explain why
it matters. Use up to three one-sentence bullets when the reviewer needs
to consider distinct changes separately.

Include a verified result, scope limit, or risk only if it affects the
reviewer's judgment. Keep it within the same summary.

Add at most one compact diagram, tree, or diff sketch when it makes an
important flow, dependency, or boundary easier to understand. Let it
carry that detail so the prose can stay short.
