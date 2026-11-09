# usability-walkthrough

An agent skill that audits the usability of a web app **by using it**: it walks every role through its real daily tasks in a real browser, finds where people get stuck, fixes the small things, verifies each fix, and hands the owner a report written for non-technical readers.

> Status: **first version**. The method was proven by hand on a production SaaS (a point-of-sale system for restaurants) on 2026-11-09: 21 findings across 4 roles, 10 fixed and tested in one session. The skill is written and tested on planning runs; its first full run on another app is next.

## Why

Complex software costs twice: users get stuck, and then someone has to get on a call, listen to the problem, interpret it and explain the screen. Most of those calls come from the same few causes: too many options in one place, screens built for a different kind of customer, and **dead ends** (a disabled button, an error or an empty screen that doesn't say what to do next).

This skill finds those causes before users do.

## The one rule

**Nothing blocks without showing the way out.** A disabled button says why. An error says what to do. If a step is missing (no products loaded, register closed, no printer), the screen offers to do it right there. Every finding is judged against this rule.

## What it does

1. **Interviews you first.** One question at a time, each with a guess attached, until it knows who the end users are, what triggered the audit and what you expect back. You don't need to know how to phrase it.
2. **Writes a short spec** with the tasks per role, the severity scale and the line between "small fix" and "structural change". You approve it before anything runs.
3. **Works in isolation.** Its own git worktree and its own copy of the app with test data, on its own ports. Never against production, never on top of another session.
4. **Walks the app as each role**, on a phone (390 px) and a desktop (1280 px): the owner on day one, the staff at rush hour, the back office at closing time. It counts taps, notes every hesitation, and **provokes the classic traps** (offline, wrong PIN, missing setup, empty states, form errors) to check that each one shows its exit.
5. **Measures, doesn't eyeball.** Load time per screen, tap targets under 44 px, disabled controls with no reason, horizontal overflow, native `alert`/`confirm` dialogs, console errors.
6. **Reports by severity** (blocking, high, medium, low), each finding with role, screen, before/after screenshots and a proposal, plus what works well and must not be touched, and what was not verified.
7. **Fixes the small things** (copy, exits, empty states, overflows) and leaves the structural ones (navigation, per-business-type setup, flow changes) as proposals with their cost, for you to decide.
8. **Verifies every fix** in the browser and with the project's test suite, and adds a regression test that is **seen failing against the old code** before it counts.

## How it differs from existing skills

Searched on skills.sh and GitHub (2026-11-09). Good related work exists, and this skill builds on its ideas:

| Skill | What it covers | What this one adds |
|---|---|---|
| [`jezweb/claude-skills` `ux-audit`](https://skills.sh/jezweb/claude-skills/ux-audit) | Live walkthrough as a user, hard QA gates (console, axe, Web Vitals) | Interview-first intent, per-role and per-business-type tasks, the "no dead ends" rule, small/structural split, fixes with red-then-green tests |
| [`wondelai/skills` `ux-heuristics`](https://skills.sh/wondelai/skills/ux-heuristics) | Krug and Nielsen heuristics, severity scale (reference) | Applies them on the running app instead of on screenshots |
| [`owl-listener/designer-skills` `heuristic-evaluation`](https://skills.sh/owl-listener/designer-skills/heuristic-evaluation) | Heuristic evaluation method | Same, plus fixing and verifying |
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
