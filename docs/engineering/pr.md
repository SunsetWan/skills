## What it does

In this fork, engineering document paths and tracker configuration are resolved through the shared project configuration reader. New AI working documents default to `docs-ai/`; existing configuration and explicit user destinations take precedence.

`pr` gives the [agent](https://www.aihero.dev/ai-coding-dictionary/agent) a format for the pull request body. One short **Summary** tells reviewers what changed and why it matters.

## When to reach for it

Type `/pr`, or the agent reaches for it automatically whenever it is writing a PR body.

| Your situation | Reach for |
| --- | --- |
| A branch is ready and needs a body a reviewer can scan | `pr` |
| The code is written but nobody has reviewed it yet | [code-review](https://aihero.dev/skills-code-review) first, then `pr` |
| The PR is open and review comments are coming back | Nothing in this set yet; `pr` only writes the body |

## The template

Most changes fit in one or two sentences under `## Summary`. Up to three one-sentence bullets can give distinct changes their own space. A single compact visual can carry details about a flow, dependency, or boundary when seeing the relationship helps the reviewer.

## Common questions

**Does it open the PR for me?**

No. `pr` covers only the body. [implement](https://aihero.dev/skills-implement) ends by committing to the current branch. Requests for a skill or option that opens the PR (a `/to-pr`, or `implement` opening a PR instead of committing) are still open proposals. One user's workaround is a one-sentence local override of `implement` that tells it to open a PR. [implement-spec](https://aihero.dev/skills-implement-spec) is the exception: it opens a draft PR when your issue tracker closes work through PRs or when you ask for one. Because `pr` is model-invoked, the agent uses this shape for the body whenever you ask it to open a PR.

**Won't it just produce another wall of text and diagrams?**

The summary starts with the change and its purpose. When a visual makes a relationship easier to understand, it takes the place of the prose that would explain that relationship.

**My repo already has a PR template. Which one wins?**

Neither, by default. `pr` has its own template and does not look for `.github/pull_request_template.md` or anything like it. Several users asked for the skill to use the repo's template. If you do nothing, the agent has two competing instructions for the same document. Settle the precedence in your repo's agent docs. This fork's default body has a single Summary section.

**Is the output HTML? Why doesn't the Mermaid diagram render?**

The output is a Markdown PR body. GitHub and GitLab can render Mermaid blocks in the description. A plain terminal shows the source of the diagram. A text tree or diff sketch is readable in both places.

**Can it sort through the review comments that come back?**

No. It writes the body and stops. Users have asked more than once for a way to triage comments from other developers or review bots (which are worth acting on, which are non-issues). This skill does not do that.

**Does it keep the body up to date as the PR changes?**

No. It writes the body at one point in time, and a PR that changes under review leaves that body stale. Ask the agent to rewrite the body after a large change. The agent is writing a PR body again, so it uses the same shape.

**My change has no UI. Does it need verification details?**

A verified result, scope limit, or risk belongs in the Summary when it affects the reviewer's judgment. The same rule applies to UI and non-UI changes.

**Can it mark the body as written by an LLM?**

Not by itself. One user's approach is a standing instruction in the repo's agent docs that every issue, comment, and PR the agent writes ends with a disclosure line. That rule belongs in the repo, where it covers everything the agent posts, rather than in a template for one kind of document.

## It's working if

- You can tell what changed and why in one short Summary.
- Any visual makes an important relationship easier to see.
- Any verification result, scope limit, or risk helps you make a review decision.

## Where it fits

`pr` comes between review and retro when the build ships as a pull request: `to-spec → to-tickets → implement → code-review → pr → retro`. It is model-invoked, so it also fires on its own any time the agent writes a PR body outside that chain.

- [code-review](https://aihero.dev/skills-code-review) runs before it, because a PR body should describe a diff that has already been reviewed.
- [implement](https://aihero.dev/skills-implement) produces the commits the body describes.

[ask-matt](https://aihero.dev/skills-ask-matt) routes across the whole set when you are unsure which skill the situation wants.
