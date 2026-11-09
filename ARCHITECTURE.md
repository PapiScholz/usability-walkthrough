# Architecture

## Overview

`usability-walkthrough` is a single agent skill: one `SKILL.md` with the method, plus a `references/` folder the agent reads only when a phase needs it. There is no code to run and no service to deploy. A thin Claude Code plugin manifest exists only so the skill can be installed with one command.

The skill runs inside the user's agent session, against the user's own project. Everything it touches (test copy of the app, browser, the report) belongs to that project. It changes no product code.

```mermaid
flowchart LR
  U[Project owner] -->|"audit the usability of this project"| A[Agent + SKILL.md]
  A -->|interview, spec| U
  A -->|isolated copy| P[User's app, test data]
  A -->|real browser, per role| P
  A -->|report with measured proposals| U
  U -->|picks proposals, new session| D[Developer implements]
```

## Components

| Component | Responsibility | Location |
|---|---|---|
| Skill | The method, phase by phase, with the gates between phases | `skills/usability-walkthrough/SKILL.md` |
| References | Interview questions, spec and report templates, trap list, severity scale, measurement snippets | `skills/usability-walkthrough/references/` |
| Plugin manifest | Makes the repo installable as a Claude Code plugin marketplace | `.claude-plugin/` |

## Data flow

1. The owner asks for an audit. The agent interviews them one question at a time until it can state who the end users are, what triggered the audit and what they expect back.
2. The agent writes a spec and waits for approval.
3. The agent starts an isolated copy of the app with test data, on its own ports (from `git archive` if the repo must stay untouched).
4. It measures each role's frequent tasks in a real browser (steps, decisions, things to ignore, waits), provokes the classic traps and measures every screen.
5. It designs the simpler version of each costly task and writes a self-contained report: proposals with measured before and after, acceptance criteria and a prompt for a new session.
6. It stops its servers and removes its temp copy. The developer later picks proposals and implements them in a fresh session.

No data leaves the user's machine because of the skill itself. The skill never targets production.

## Where things live

| Path | What |
|---|---|
| `README.md` | What the skill is, how to install and use it |
| `skills/usability-walkthrough/` | The skill |
| `docs/adr/` | Decisions |

## External services

None at runtime. Distribution through GitHub (plugin marketplace) and [skills.sh](https://skills.sh/).

## Decisions

- [ADR-0001: Ship as a plain skill, packaged only for installation](docs/adr/0001-ship-as-a-plain-skill.md)
