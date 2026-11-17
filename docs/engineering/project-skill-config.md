## What it does

Resolves a project's tracker, label mapping, and document paths before an engineering skill reads or writes them. It reads configuration without initializing or migrating the project.

## When to reach for it

The engineering skills invoke it automatically. Invoke it directly to inspect which configuration and document paths will be used.

## Common questions

**Will old projects be moved into docs-ai automatically?**

No. Existing configuration and legacy documents remain usable in place. A setup run must present an explicit migration plan before moving them.

**Does ignoring docs-ai prevent remote issues?**

No. Git ignore controls file tracking. Remote publication follows the separately selected tracker and the user's task authorization.

## It's working if

- A standalone spec or domain-modeling invocation finds the same configuration as setup.
- New local working documents stay under ignored `docs-ai/` paths.
- Existing projects retain their document locations and explicit deliverable paths are honored.

## Where it fits

This is shared runtime configuration for the engineering flow. Setup writes its inputs; consumers use its resolved destinations. The [skill router](https://github.com/SunsetWan/skills/blob/sunset/docs-ai/skills/engineering/ask-matt/SKILL.md) describes the surrounding workflows.
