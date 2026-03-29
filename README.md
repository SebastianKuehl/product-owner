# Product Owner Agent

A chat mode for GitHub Copilot CLI that acts as your AI product owner — planning, orchestrating, reviewing, and releasing, so your team (of humans and agents) stays on track.

## Install

```
copilot plugin install SebastianKuehl/product-owner
```

Then run `copilot` and select the **product-owner** agent.

## What It Does

The Product Owner Agent owns the full delivery lifecycle:

- **Scope & planning** — Converts your plan into structured `docs/` with scope, milestones, features, and bugs
- **Work decomposition** — Breaks milestones into focused, agent-sized tasks with clear acceptance criteria
- **Orchestration** — Launches [Anvil](https://github.com/burkeholland/anvil) agents in the background for implementation work
- **Review & merge** — Reviews completed work against acceptance criteria, merges to `main`, and blocks unfinished work
- **Release tagging** — Tags semver releases on `main` with changelog entries in `docs/releases.md`
- **README governance** — Keeps `README.md` aligned with merged, shipped functionality — never with unmerged work

## How It Works

1. Describe your project or drop in a feature/bug/milestone request
2. The agent classifies the input, creates or updates `docs/` accordingly
3. Worker prompts are created in `docs/prompts/` and Anvil agents are launched
4. Completed work is reviewed against acceptance criteria
5. Accepted work is merged, tagged, and documented

## Project Structure

```
docs/
  scope.md              # Project summary, constraints, success criteria
  worker-agent-rules.md # Rules governing all delegated Anvil agents
  progress.md           # Operational ledger — every item, status, and assignment
  releases.md           # Semver changelog
  milestones/           # M-001-*.md  — delivery phases
  features/             # F-001-*.md  — capabilities
  bugs/                 # B-001-*.md  — defects
  prompts/              # P-001-*.md  — worker prompts for Anvil agents
```

## Chain of Command

```
Instructor
  └── Product Owner Agent
        └── Anvil agents (implementation only)
```

Anvil agents may not merge to `main`, tag releases, or edit `README.md`. Only the Product Owner Agent and the instructor may do those things.

## License

MIT
