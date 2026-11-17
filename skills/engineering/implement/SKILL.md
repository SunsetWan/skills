---
name: implement
description: "Implement a piece of work based on a spec or set of tickets."
disable-model-invocation: true
---

Call the Skill tool with "project-skill-config" before reading or writing project documents. If this harness has no Skill tool, load that installed skill's `SKILL.md` through skill discovery. Use its resolved tracker, labels, and document paths throughout this skill and pass them to subagents.

Implement the work described by the user in the spec or tickets.

If the user passes a ticket reference, fetch it from the issue tracker and state its title before starting. If the reference is ambiguous, ask.

Call the Skill tool with "tdd" where possible, at pre-agreed seams.

Run typechecking regularly, single test files regularly, and the full test suite once at the end.

Once done, call the Skill tool with "code-review" to review the work.

Commit your work to the current branch.
