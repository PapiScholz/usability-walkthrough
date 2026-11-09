---
name: usability-walkthrough
description: Use when the owner of a web app asks for a usability or UX audit, says users find the software confusing or cumbersome, support calls take too long explaining screens, or wants the app to feel intuitive and fast for every role that uses it.
---

# Usability Walkthrough

## Overview

Audit usability by **using the app** as each of its real users, not by reading its code. One rule judges every screen: **nothing blocks without showing the way out.** A disabled button says why, an error says what to do, a missing step (no data loaded, register closed, no printer) is offered right there.

A finding exists only if you saw it in the running app. Code reading and grep produce *leads* to check in the browser, never findings.

Out of scope: whether the app has the right features (utility), visual redesign, and testing with real people. Note feature gaps you stumble on as a one-line aside, never as findings.

## Phases (each one ends at a gate)

1. **Interview.** One question per message, each with your guess attached, until you can state: who the end users and roles are, which kinds of customers use it (a bakery is not a restaurant), what triggered the audit, what to deliver, what is out of scope. Then restate it and wait for an explicit yes. Questions and restate: `references/interview.md`. Read what users already said (support tickets, feedback tables, error logs, existing audits, the help docs): those are leads, and they rank the findings later.
2. **Spec.** Write it in the project's spec location (or `docs/usability/SPEC.md`) using `references/spec-template.md`: tasks per role, traps, severity scale, the small-vs-structural line, boundaries. Wait for approval.
3. **Isolate.** Own git worktree. Own copy of the app with test data, on free ports, never production and never another session's copy. Seed realistic data through the app's API or test helpers, one dataset per kind of customer.
4. **Walk.** In a real browser (Playwright or Chrome DevTools MCP), as each role, at the screen size that role really uses (the repo's docs or the interview say so; default 390 px and 1280 px, plus tablet for kitchen/back-office screens). Desktop app (Electron, Tauri): walk its web build if it has one and list what only the packaged app can show (printer, updater, native menus) as not verified. Do every task in the spec; count taps; screenshot before acting; note every moment of doubt. Provoke every trap in `references/traps.md` and record whether its exit shows. Run the measurement snippet in `references/measure.md` on every screen.
5. **Report.** `references/report-template.md`: severity, role, screen, screenshot, what the user experiences, proposal; what already works (don't touch); what was not verified.
6. **Fix the small ones.** Copy, exits, empty states, overflow, tap targets, native dialogs on frequent paths. Anything that touches more than one screen or changes what users already learned is **structural**: propose it with cost, don't build it.
7. **Verify.** Each fix seen in the browser at both widths. Add a regression test and **watch it fail against the old code** (serve the base branch from `git archive` in a temp folder; don't revert your work). Run the project's type check and browser suite.
8. **Close.** Stop every server you started (whole process tree, then check the ports), delete tool artifacts the browser tool left in the repo (e.g. `.playwright-mcp/`), and hand over the report path. No commit or push unless the user asks in that turn.

## Severity

| Level | Meaning |
|---|---|
| Blocking | Can't finish the task, or no visible way out |
| High | Finishes with doubt, extra steps on a frequent task, or risk of a costly mistake (wrong charge, lost order) |
| Medium | Confuses or annoys once: unclear label, misplaced control, silent wait |
| Low | Polish and consistency |

## Common mistakes

| Mistake | Instead |
|---|---|
| Asking three questions at once, then starting anyway | One question, one guess, wait |
| Reporting file sizes, `@media` counts or grep hits as findings | Treat them as leads; confirm in the browser or drop them |
| Walking only the owner on desktop | Every role, on the device that role really uses |
| One kind of customer | One seeded dataset per kind; check onboarding, templates and empty states for each |
| Fixing structural issues because "it's obviously better" | Propose with cost; the owner decides |
| A regression test that never failed | Run it against the base branch first |
| "Looks fine" on a trap you didn't trigger | Trigger it; screenshot the exit or report its absence |
| Leaving the dev server running | Kill the tree, verify the port is free |
