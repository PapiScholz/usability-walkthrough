# Traps to provoke

Trigger each one that applies. For each, record: what the user sees, whether the exit is visible, and a screenshot.

| Trap | Expected exit |
|---|---|
| Main action with a prerequisite missing (register closed, no products, no printer, no payment method) | The message names the missing step and offers to do it, or says who can |
| Empty state on first use | What goes here + the button to add the first one |
| Role without permission reaches a screen or message meant for another role | It says who can do it, never a link the role can't open |
| Wrong credentials, PIN or code | Which one is wrong (when safe) and how to change it |
| Form with errors | Error next to the field, in plain words, nothing lost |
| Network drops mid-task | What was saved, what happens when it returns, and the message updates when it does |
| Feature not in the plan | What it does and how to get it |
| Destructive action | Undo, or a confirmation inside the app that says the consequence |
| Long or failed wait | Visible progress; on failure, retry |
| Success | Visible confirmation where the user is looking (not a native `alert`, not off-screen) |

Also check per kind of customer: onboarding steps that don't apply can be skipped; templates and defaults fit that business.
