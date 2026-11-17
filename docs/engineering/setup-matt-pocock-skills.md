## What it does

Configures a project's issue tracker, triage labels, and domain document paths. This fork writes new configuration to `docs-ai/agents/` and protects local AI documents with Git ignore rules. It leaves root agent instructions unchanged because consumers discover configuration through the shared reader.

## When to reach for it

Invoke `/setup-matt-pocock-skills` before the first engineering workflow, to change the selected tracker, or to request a deliberate migration. Setup reuses already approved choices and shows unresolved choices before writing.

## Common questions

**Can tasks stay local even when the repository has a GitLab remote?**

Yes. Choose local Markdown. New tasks then live under `docs-ai/tasks/`; no remote issues or labels are created by local setup.

**What happens to existing docs/agents, .scratch, or Context files?**

They remain readable in place. Setup moves them only after an explicit migration plan is approved. Already tracked files require an intentional tracking change; adding an ignore rule alone does not make them private.

**Can a project choose different paths?**

Yes. Applicable project instructions can select a configuration directory, and the configuration can specify document destinations. An explicit user deliverable path wins over defaults.

## It's working if

- The configured local paths are ignored and not tracked or staged.
- Independently invoked engineering skills discover the same tracker and domain paths.
- Existing root agent instructions and unrelated documentation remain unchanged.

## Where it fits

This is run-once project setup. The [shared reader](https://github.com/SunsetWan/skills/blob/sunset/docs-ai/skills/engineering/project-skill-config/SKILL.md) provides configuration to consumers, and [ask-matt](https://aihero.dev/skills-ask-matt) routes the engineering flow.
