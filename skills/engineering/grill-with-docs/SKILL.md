---
name: grill-with-docs
description: A relentless interview to sharpen a plan or design, which also creates docs (ADR's and glossary) as we go.
disable-model-invocation: true
---

Call the Skill tool with "project-skill-config" before reading or writing project documents. If this harness has no Skill tool, load that installed skill's `SKILL.md` through skill discovery. Use its resolved tracker, labels, and document paths throughout this skill and pass them to subagents.

Call the Skill tool twice, for "grilling" and "domain-modeling".
