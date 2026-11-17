# Local AI documentation policy

This fork defaults engineering configuration and working documents to `docs-ai/`. The shared model-invoked `project-skill-config` skill owns precedence and migration boundaries. Install it together with consumers; installing setup alone does not redirect their reads or writes.

## Review cases

| Case | Expected resolution |
| --- | --- |
| Fresh project | New config under `docs-ai/agents/`; local tasks under `docs-ai/tasks/`; domain files created lazily |
| Standalone consumer, no root agent file | Explicit consumer call loads the reader and discovers config |
| Existing `docs/agents/` and `.scratch/` | Read legacy config and paths in place; no migration |
| Both new and legacy config | New corresponding file wins; report material conflicts, do not merge |
| Explicit project paths, destination absent | Keep configured paths; lazily create them instead of falling back |
| Legacy `CONTEXT.md` or context map | Read in place until an explicit migration is approved |
| Explicit deliverable or teaching workspace | Preserve user destination |
| GitLab remote, local tracker selected | Write local tasks; no remote issues or labels |
| Configured remote tracker | Keep selected remote workflow; ignore rules do not authorize publication |
| Already tracked `docs-ai/` files | Report tracking and obtain migration/untracking authorization |
| Subdirectory or submodule invocation | Resolve paths from the owning repository root |

These are prompt-policy review cases, not automated model-behavior tests. Static verification checks consumer entry points, registration, metadata, and documentation. Native plugin validation succeeds with the upstream warning that root `CLAUDE.md` is not loaded as plugin context; strict mode rejects that pre-existing warning. The shared reader supplies runtime configuration independently of that root file.

Managed installation should pin the fork commit, update only the affected skill snapshots and provenance, preserve machine-local differences, and verify canonical content and both agent links. Upstream synchronization requires reviewing this policy and the affected consumers before deploying a new pin.
