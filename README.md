# usability-walkthrough

An agent skill that audits the usability of a web app **by using it**: it walks every role through its real daily tasks in a real browser, measures how many steps and decisions each one costs, finds where people get stuck, and hands over a report of measured proposals that the developer implements later, in a fresh session.

> Status: **first version**. The method was proven by hand on a production SaaS (a point-of-sale system for restaurants) on 2026-11-09: 21 findings across 4 roles. A trial run on a second app (a shop point of sale) found 8 more in 30 minutes without touching its repo. Since then the skill puts measured simplifications first and stops at the report.

## Why

Complex software costs twice: users get stuck, and then someone has to get on a call, listen to the problem, interpret it and explain the screen. Most of those calls come from the same few causes: too many options in one place, screens built for a different kind of customer, and **dead ends** (a disabled button, an error or an empty screen that doesn't say what to do next).

This skill finds those causes before users do. What users notice most is doing the same with less: fewer steps, fewer decisions, fewer things on screen in the tasks they repeat every day. So the report leads with that, measured.

## The rule every screen must pass

**Nothing blocks without showing the way out.** A disabled button says why. An error says what to do. If a step is missing (no products loaded, register closed, no printer), the screen offers to do it right there. Every dead end is judged against this rule.

## What it does

1. **Interviews you first.** One question at a time, each with a guess attached, until it knows who the end users are, the kinds of customers, each role's frequent tasks and what triggered the audit. You don't need to know how to phrase it.
2. **Writes a short spec** with the frequent tasks per role, the traps and the boundaries. You approve it before anything runs.
3. **Works in isolation.** Its own copy of the app with test data, on its own ports. Never against production, never on top of another session; the repo can stay untouched.
4. **Measures the frequent tasks** as each role, on the device that role really uses: steps, decisions, things to ignore on screen, waits. Screenshots of every step.
5. **Provokes the classic traps** (offline, wrong PIN, missing setup, empty states, form errors) to check that each one shows its exit, and measures every screen (tap targets, disabled controls with no reason, overflow, native dialogs).
6. **Designs the simpler version** of each costly task with a target ("sell and charge: 7 steps → 3"), using five levers: remove, default, merge, adapt to the kind of customer, hide what's rare.
7. **Writes the report.** Proposals ranked by how often the task happens × steps saved. Each one stands alone, with the measured before, the target, where in the code, acceptance criteria, how to verify, cost, risk and a ready-to-paste prompt for a new session. Then the dead ends and confusing words, what works well (don't touch) and what wasn't verified.
8. **Changes no product code.** An audit fills the context; the developer picks proposals from the report and implements them in a fresh session.

## How it differs from existing skills

Searched on skills.sh and GitHub (2026-11-09). Good related work exists, and this skill builds on its ideas:

| Skill | What it covers | What this one adds |
|---|---|---|
| [`jezweb/claude-skills` `ux-audit`](https://skills.sh/jezweb/claude-skills/ux-audit) | Live walkthrough as a user, hard QA gates (console, axe, Web Vitals) | Interview-first intent, per-role and per-business-type tasks, measured simplifications with before/after, the "no dead ends" rule, proposals ready for a fresh session |
| [`wondelai/skills` `ux-heuristics`](https://skills.sh/wondelai/skills/ux-heuristics) | Krug and Nielsen heuristics, severity scale (reference) | Applies them on the running app instead of on screenshots |
| [`owl-listener/designer-skills` `heuristic-evaluation`](https://skills.sh/owl-listener/designer-skills/heuristic-evaluation) | Heuristic evaluation method | Same, plus measuring steps on the running app |
| [`mastepanoski/claude-skills` `ux-audit-rethink`](https://skills.sh/mastepanoski/claude-skills/ux-audit-rethink) | Holistic UX strategy from descriptions and screenshots | Evidence from real interaction, scoped to what blocks users today |

## Structure

```
.claude-plugin/        plugin.json + marketplace.json (installable as a Claude Code plugin)
skills/usability-walkthrough/
  SKILL.md             the method, phase by phase, with a gate at the end of each phase
  references/          interview.md, spec-template.md, traps.md, measure.md,
                       report-template.md
docs/adr/              decisions
README.md
LICENSE.md
```

## Install

```bash
claude plugin marketplace add PapiScholz/usability-walkthrough
claude plugin install usability-walkthrough@usability-walkthrough
```

## Use

> Audit the usability of this project. My end users are … and what bothers me is …

The skill takes it from there with its first question.

## Documentation

- [Architecture](ARCHITECTURE.md) · [Decisions](docs/adr/) · [Roadmap](ROADMAP.md)
- [Security](SECURITY.md) · [Contributing](CONTRIBUTING.md) · [Code of Conduct](CODE_OF_CONDUCT.md)
- Design: does not apply (the skill has no user interface).

## License

[MIT](LICENSE.md)
