## What it does

In this fork, engineering document paths and tracker configuration are resolved through the shared project configuration reader. New AI working documents default to `docs-ai/`; existing configuration and explicit user destinations take precedence.

`pr` defines a pull request body with a single **Summary** section that shows the change and explains its purpose. Verification results and risks are optional, brief additions within Summary when they help explain the change. It is a format reference, not a workflow. It does not push a branch, open the PR, or decide what goes into it. It tells the [agent](https://www.aihero.dev/ai-coding-dictionary/agent) what the body should look like when it writes one.

The summary is a visual, not a paragraph. A default PR body describes the diff in prose. This one picks the **smallest view** that makes the key point clear (pseudocode, a call tree, a component tree, a file tree, a Mermaid diagram, or a shaped diff) and keeps the words around it brief. The reviewer already has the diff open, so the body shows them its shape before they read it.

## When to reach for it

Type `/pr`, or the agent reaches for it automatically whenever it is writing a PR body.

| Your situation | Reach for |
| --- | --- |
| A branch is ready and needs a body a reviewer can scan | `pr` |
| The code is written but nobody has reviewed it yet | [code-review](https://aihero.dev/skills-code-review) first, then `pr` |
| The PR is open and review comments are coming back | Nothing in this set yet; `pr` only writes the body |

## The template

The body contains one `## Summary` section. Place one or more small visuals next to the short text they support. Use one, sometimes several, rarely all of them. Keep only the calls, files, props, and boundaries the reviewer needs.

Describe what changed and why. Include a verification result or risk briefly within Summary only when it helps explain the change.

## Common questions

**Does it open the PR for me?**

No. `pr` covers only the body. [implement](https://aihero.dev/skills-implement) ends by committing to the current branch. Requests for a skill or option that opens the PR (a `/to-pr`, or `implement` opening a PR instead of committing) are still open proposals. One user's workaround is a one-sentence local override of `implement` that tells it to open a PR. [implement-spec](https://aihero.dev/skills-implement-spec) is the exception: it opens a draft PR when your issue tracker closes work through PRs or when you ask for one. Because `pr` is model-invoked, the agent uses this shape for the body whenever you ask it to open a PR.

**Won't it just produce another wall of text and diagrams?**

The skill tells the agent to skip preambles, keep prose brief, and pick the smallest view, usually one visual and rarely all of them. Verification and risk details are optional. If you still get a stack of diagrams, the agent has ignored that guidance. If the body is huge because the diff is huge, the problem is the size of the PR, and `pr` will not split it for you.

**My repo already has a PR template. Which one wins?**

Neither, by default. `pr` has its own template and does not look for `.github/pull_request_template.md` or anything like it. Several users asked for the skill to use the repo's template. If you do nothing, the agent has two competing instructions for the same document. Settle the precedence in your repo's agent docs. This fork's default body has a single Summary section.

**Is the output HTML? Why doesn't the Mermaid diagram render?**

The output is a markdown PR body, not an HTML page. GitHub and GitLab render Mermaid blocks in a PR description, but a terminal does not, so the diagram looks like raw text while the agent is still showing it to you locally. Users on CLI harnesses have worked around that with an ASCII Mermaid renderer or by having the agent attach an HTML version to the PR. Mermaid is one of six views. A call tree, file tree or shaped diff reads the same everywhere.

**Can it sort through the review comments that come back?**

No. It writes the body and stops. Users have asked more than once for a way to triage comments from other developers or review bots (which are worth acting on, which are non-issues). This skill does not do that.

**Does it keep the body up to date as the PR changes?**

No. It writes the body at one point in time, and a PR that changes under review leaves that body stale. Ask the agent to rewrite the body after a large change. The agent is writing a PR body again, so it uses the same shape.

**My change has no UI. Does it need verification details?**

Verification results and risks are optional for every PR. When a test result or console output helps explain a migration, a background job, or a refactor, mention it briefly within Summary.

**Can it mark the body as written by an LLM?**

Not by itself. One user's approach is a standing instruction in the repo's agent docs that every issue, comment, and PR the agent writes ends with a disclosure line. That rule belongs in the repo, where it covers everything the agent posts, rather than in a template for one kind of document.

## It's working if

- You can tell what the PR changes from the Summary visual alone, before opening the diff.
- The body has one Summary section and no preamble.
- Verification and risk details appear only when they help explain the change, briefly within Summary.

## Where it fits

`pr` comes between review and retro when the build ships as a pull request: `to-spec → to-tickets → implement → code-review → pr → retro`. It is model-invoked, so it also fires on its own any time the agent writes a PR body outside that chain.

- [code-review](https://aihero.dev/skills-code-review) runs before it, because a PR body should describe a diff that has already been reviewed.
- [implement](https://aihero.dev/skills-implement) produces the commits the body describes.

[ask-matt](https://aihero.dev/skills-ask-matt) routes across the whole set when you are unsure which skill the situation wants.
