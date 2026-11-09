# Interview

Goal: find out what the owner needs even when they can't say it directly. Ask **one question per message**, always with your guess and the reasoning behind it, so they only have to react.

```
My read: <one sentence>. Confidence: ~40% (missing: <what>).

Question: <one question>
My guess: <answer + why>. If it's <alternative>, the audit changes because <...>.
```

## What you need, in this order

| # | Topic | Typical question |
|---|---|---|
| 1 | Who the end user is | "When you picture a frustrated user, who is it and what are they doing?" Offer the roles you found in the code |
| 2 | Kinds of customers | "Is it always <X>, or also <Y, Z>?" (a bakery, a bar and a buffet use the same app differently) |
| 3 | Trigger | "Did something specific happen, or is it preventive?" If the owner themselves gets lost, that's the best signal |
| 4 | Where it hurts | "Is it more that you can't **find** things, or that **doing** them takes too many steps, or that screens don't **make sense**?" |
| 5 | Frequent tasks | "What does each role do many times a day?" Guess from the code and the help docs; these get measured first |

Stop when you can predict their answer to your next three questions.

## Restate (needs an explicit yes)

- Outcome · Users and devices · Kinds of customers · Why now
- How we'll know it worked (the phases and the report)
- Boundaries (isolated copy, no product code changes, no commit or push)
- Out of scope (always fill it)

"Sounds good" or "whatever you think" is not a yes: offer two concrete options.
