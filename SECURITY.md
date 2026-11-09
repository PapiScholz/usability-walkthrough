# Security

## Reporting a vulnerability

Use GitHub's private reporting form: <https://github.com/PapiScholz/usability-walkthrough/security/advisories/new>. Include what you ran, what happened and what you expected. Expect a first answer within 7 days.

Do not open public issues for vulnerabilities.

## What to watch for

This repository holds instructions for an agent, not running code. The relevant risks are in what those instructions make an agent do in someone else's project:

| Risk | How the skill guards against it |
|---|---|
| Acting on production data or real accounts | The method requires an isolated copy with test data and forbids targeting production |
| Overwriting the user's work | The audit changes no product code; the only file it writes is the report, and no commit or push without the user's explicit request |
| Leaking secrets into reports or screenshots | Reports and screenshots come from test data only |
| Leaving processes running on the user's machine | The method ends by stopping every server it started |

If you find an instruction that can lead an agent to break one of these, report it privately as above.

## Secrets

The repository has no secrets and needs none.
