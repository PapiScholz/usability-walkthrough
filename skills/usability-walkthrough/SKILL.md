---
name: usability-walkthrough
description: Use when the owner of a web app asks for a usability or UX audit, says users find the software confusing or cumbersome, support calls take too long explaining screens, or wants the app to feel simpler, more intuitive and faster for every role that uses it.
---

# Usability Walkthrough

## Overview

Audit ease of use by **using the app** as each of its real users, and deliver a report of proposals the developer can implement later, in a fresh session. The audit changes no product code.

What users notice is **doing the same with less**: fewer steps, fewer decisions, fewer things on screen in the tasks they repeat every day. So the report leads with measured simplifications ("sell and charge: 7 steps → 3"). Second comes the rule every screen must pass: **nothing blocks without showing the way out.**

A finding exists only if you saw it in the running app. Code reading and grep produce *leads* to check in the browser, never findings.

Out of scope: implementing the proposals, whether the app has the right features (utility), visual redesign, and testing with real people. Note feature gaps you stumble on as a one-line aside.

## Phases (each one ends at a gate)

1. **Interview.** One question per message, each with your guess attached, until you can state: who the end users and roles are, which kinds of customers use it (a bakery is not a restaurant), each role's most frequent tasks, what triggered the audit, what is out of scope. Then restate it and wait for an explicit yes. See `references/interview.md`. Read what users already said (support tickets, feedback, error logs, help docs): those are leads, and they rank the proposals later.
2. **Spec.** Write it with `references/spec-template.md`: frequent tasks per role, traps, viewports, boundaries, where the report goes. Wait for approval.
3. **Isolate.** Your own copy of the app with test data, on free ports, never production and never another session's copy. If the repo must stay untouched, export it with `git archive` to a temp folder. Seed realistic data, one dataset per kind of customer, and reproduce the state a real install or signup ships (flags, settings).
4. **Measure the frequent tasks.** In a real browser (Playwright or Chrome DevTools MCP), as each role, at the screen size that role really uses (the repo or the interview says so; default 390 px and 1280 px). For every frequent task count: steps (taps, keys, screens), decisions the user must make, things on screen they must ignore, and waits. Type at human speed. Screenshot each step.
5. **Provoke the traps** in `references/traps.md` and record whether each exit shows. Run `references/measure.md` on every screen.
6. **Design the simpler version** of each costly task, with a target ("first sale within 5 minutes of installing, unaided"). Levers, strongest first:
   - remove what this role or business never uses;
   - smart defaults instead of questions;
   - merge screens and steps;
   - adapt setup and screens to the kind of customer;
   - move rare options behind "More options".
7. **Report.** `references/report-template.md`. Proposals are ranked by frequency × steps saved. Each one stands alone: measured before, target after, levers, files likely touched, acceptance criteria, how to verify, cost and risk, and a ready-to-paste prompt for a new session. Below them go the dead ends and confusing words, then what works well (don't touch) and what wasn't verified.
8. **Close.** Stop every server you started (whole process tree, then check the ports), delete tool artifacts (e.g. `.playwright-mcp/`), the temp copy and test data, and hand over the report path. No commit or push unless the user asks in that turn.

## Severity (for dead ends and wording)

| Level | Meaning |
|---|---|
| Blocking | Can't finish the task, or no visible way out |
| High | Risk of a costly mistake (wrong charge, lost order) or extra steps on a frequent task |
| Medium | Confuses or annoys once: unclear label, misplaced control, silent wait |
| Low | Polish and consistency |

## Common mistakes

| Mistake | Instead |
|---|---|
| A report of small defects only | Lead with measured simplifications of frequent tasks; that is what users notice |
| "Simplify the checkout" with no numbers | Before and after in steps, decisions and screens |
| Implementing proposals during the audit | Report only; the context is spent, the developer implements in a fresh session |
| A proposal that needs the audit chat to be understood | Self-contained: files, acceptance criteria, verification, prompt |
| Asking three questions at once, then starting anyway | One question, one guess, wait |
| Reporting file sizes, `@media` counts or grep hits as findings | Treat them as leads; confirm in the browser or drop them |
| Walking only the owner on desktop | Every role, on the device that role really uses |
| One kind of customer | One dataset per kind; check onboarding, templates and empty states for each |
| Filling fields instantly (`fill`) and reporting what happens | Type at human speed (`pressSequentially`, ~100 ms): instant input can trigger barcode-scanner or autocomplete logic a person never hits |
| Testing first run on a dev seed | Reproduce what the installer or signup really ships; a dev seed can skip onboarding and fake a finding |
| "Looks fine" on a trap you didn't trigger | Trigger it; screenshot the exit or report its absence |
| Leaving the dev server running | Kill the tree, verify the port is free |
