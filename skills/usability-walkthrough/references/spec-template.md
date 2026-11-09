# Spec: usability walkthrough

## 1. Objective
Who uses it, why now, the rule ("nothing blocks without showing the way out"), and what "done" means:
1. Every task in section 4 walked per role at 390 and 1280 px, with taps, doubts and exits recorded.
2. A report with every finding (severity, role, screen, screenshot, proposal).
3. Small findings fixed and verified; structural ones proposed with cost.

## 2. Assumptions (correct before approving)
Scope (which apps or areas), devices per role, test data, plan or feature flags, ports.

## 3. Method
Inventory (what each role sees and lands on) → walkthrough → heuristics (Nielsen; focus on status visibility and error recovery) → consistency → basic accessibility (44 px targets, contrast, focus) → speed measured inside the page.

## 4. Tasks per role
Frequent tasks first. For each role: the daily tasks and the first-day setup tasks. Then the traps from `traps.md` that apply.

## 5. Severity
Blocking / High / Medium / Low (see SKILL.md).

## 6. Small vs structural
| Small: fix now | Structural: propose |
|---|---|
| Copy, labels, errors with an exit | Navigation or menu reorganization |
| Disabled controls that say why | Per-customer-type setup |
| Empty states with the action | Removing, merging or renaming modules |
| Loading and confirmation states | Changing a whole flow |
| Tap targets, focus, contrast, overflow | API or database changes |

If a change touches more than one screen or changes what users already learned, it's structural.

## 7. Commands and structure
Real commands from the repo: start the isolated copy, type check, test suites. Where the report, screenshots and new tests go.

## 8. Boundaries
Always / Ask first / Never — including other sessions' files and production.

## 9. Open questions
