# Usability report

Spec: <link>. Date: <YYYY-MM-DD>. App version / commit audited: <...>.

Write it for a developer who was not in the audit and opens it in a fresh session. Nothing here may depend on the audit conversation.

## How it was done
Environment (isolated copy, never production), viewports per role, datasets per kind of customer, roles walked, traps provoked. Screenshots in `<folder>/`, named `<task>-<step>.png`.

**Already works well (don't touch):** <list>

## Summary
| Task | Role | Done per day (estimate) | Today | Target | Proposal |
|---|---|---|---|---|---|
| Sell and charge in cash | Cashier | many | 7 steps, 2 decisions | 3 steps, 0 decisions | P1 |

One paragraph: what the end user will notice most if P1 to P3 are done.

## Proposals (ranked by frequency × steps saved)

### P1. <The task, said the way the user would say it>
- **Who and how often:** <role, device, frequency>
- **Today (measured):** step by step, with screenshots: `sell-01.png` … Steps: N · decisions: N · things to ignore on screen: N · waits: N
- **Target:** step by step. Steps: N · decisions: N
- **Levers:** remove · default · merge · adapt to customer kind · hide advanced
- **Where in the code:** files and components likely touched (verify before editing)
- **Acceptance criteria:** observable, testable statements ("a cashier with one payment method never sees the method picker")
- **How to verify:** the browser test to write, and that it must fail on the current code first
- **Cost and risk:** S / M / L; what could break; what users must relearn
- **Prompt for a new session:**
  ```
  Implement proposal P1 from <report path>. Read only that section and the files it names.
  Work in a branch, write the acceptance test first and watch it fail, then implement,
  verify in the browser at <viewport>, run <type check and test commands>. No push.
  ```

(P2, P3… the same way.)

## Dead ends and wording
| # | Severity | Role · screen | What the user experiences | Exit it should show | Screenshot |
|---|---|---|---|---|---|

## Leads not confirmed
Things suspected but not reproduced in the browser, with how to check them.

## Not verified
Real devices, packaged app paths, production latency, screen readers, tasks not walked.
