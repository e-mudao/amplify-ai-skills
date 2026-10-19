# Amplify AI Skills

**Turn rough ideas into clear, useful results.**

Ten Agent Skills for working with AI. Start with the point where you're stuck—framing a request, researching a question, making a decision, writing, checking an answer, or improving a draft—and choose the skill that fits.

**Language:** [简体中文](README.md) · English

## Start with what you need

| You need to… | Start with | What you get |
| --- | --- | --- |
| Turn scattered ideas into a clear request | [`clarify`](skills/amplify-ai-clarify/SKILL.md) | Clear requirements or a task ready to continue |
| Raise the ambition, depth, or breadth of a goal | [`ambition`](skills/amplify-ai-ambition/SKILL.md) | A more valuable, actionable, testable task framing |
| Prioritize, sequence, or revise a plan | [`plan`](skills/amplify-ai-plan/SKILL.md) | An adaptable plan that accounts for dependencies and trade-offs |
| Choose among options | [`decide`](skills/amplify-ai-decide/SKILL.md) | A recommendation grounded in your goals and constraints |
| Investigate an open question | [`research`](skills/amplify-ai-research/SKILL.md) | A sourced answer with important limitations |
| Extract the essentials from existing material | [`distill`](skills/amplify-ai-distill/SKILL.md) | A synthesis that preserves conditions, disagreements, and sources |
| Turn ideas into ready-to-use text | [`write`](skills/amplify-ai-write/SKILL.md) | A draft suited to its audience and context |
| Check claims, citations, figures, or code behavior | [`verification`](skills/amplify-ai-verification/SKILL.md) | An evidence-based verdict with stated limits |
| Revise an existing result from feedback | [`refine`](skills/amplify-ai-refine/SKILL.md) | Focused changes that preserve what works |
| Help an audience understand a topic | [`explain`](skills/amplify-ai-explain/SKILL.md) | An explanation or demonstration suited to the learning goal |

> **Rule of thumb:** Pick a skill for your current bottleneck. If one skill can do the job, there is no need to chain several together.

## Quick start

Each skill is a standalone directory with a `SKILL.md` entry point. The skills themselves require no dependencies or API key. From the repository root:

**Codex: install all ten skills**

```bash
mkdir -p "$HOME/.agents/skills"
cp -R skills/amplify-ai-* "$HOME/.agents/skills/"
```

To install just one, for example `plan`:

```bash
cp -R skills/amplify-ai-plan "$HOME/.agents/skills/"
```

**Claude Code: install all ten skills**

```bash
mkdir -p "$HOME/.claude/skills"
cp -R skills/amplify-ai-* "$HOME/.claude/skills/"
```

For a Claude Code project installation, copy them into that project's `.claude/skills/` directory. With other hosts, place the directories wherever the host loads skills, or ask the agent to read `skills/<name>/SKILL.md` directly. Follow your host's documentation for loading and invocation.

Then describe your task, or name a skill explicitly:

> Use `amplify-ai-plan` to prioritize this work and identify the next steps.

Automatic skill selection depends on the host's skills support and configuration.

## How the skills fit together

| Common path | When it helps |
| --- | --- |
| `clarify` → `plan` / `decide` | Define the goal, then organize the work or choose a direction |
| `research` → `verification` → `distill` / `write` | Build an answer, check key claims, then make it useful to a reader |
| `write` → `refine` | Draft from ideas and source material, then revise from feedback |
| `explain` | Choose writing, diagrams, an interactive page, or video to support understanding |

Similar names, different jobs:

- **`clarify` / `distill`:** Clarify a request or question; synthesize material you already have.
- **`research` / `verification`:** Investigate an open question; check an existing claim or result.
- **`write` / `refine`:** Create a draft from an intention and source material; revise an existing artifact from feedback.
- **`write` / `explain`:** Produce text ready to use; help an audience understand a topic.

## Repository and license

- [`skills/`](skills/): Ten standalone skill directories with their own `SKILL.md` and license files.
- [`LICENSE`](LICENSE): The repository's MIT license. Check the license inside each skill directory when using an individual skill.

To update a skill, copy its directory again. To uninstall it, remove the corresponding directory from your host's skills location.
