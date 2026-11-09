# Spec: usability walkthrough

## 1. Objective
Who uses it, why now, and what "done" means:
1. Every frequent task in section 4 measured per role, on that role's device: steps, decisions, things to ignore, waits.
2. A simpler version designed for each costly task, with a measured target.
3. Every trap in section 5 provoked, with its exit recorded.
4. A self-contained report the developer can implement from in a fresh session. No product code changes during the audit.

## 2. Assumptions (correct before approving)
Scope (which apps or areas), devices and viewports per role, kinds of customers and their datasets, plan or feature flags, the first-run state a real install ships, ports.

## 3. Method
Inventory (what each role sees and lands on) → measure frequent tasks → provoke traps → per-screen measurement (`measure.md`) → design the simpler version with the levers (remove, default, merge, adapt, hide) → report.

## 4. Frequent tasks per role
| Role | Device | Task | How often |
|---|---|---|---|

Daily tasks first, then the first-day setup.

## 5. Traps
The ones from `traps.md` that apply to this app.

## 6. Commands and structure
Real commands to start the isolated copy and seed it. Where the report and screenshots go (default `docs/usability/`).

## 7. Boundaries
Always / Ask first / Never — including the repo state (untouched?), other sessions' files and production.

## 8. Open questions
