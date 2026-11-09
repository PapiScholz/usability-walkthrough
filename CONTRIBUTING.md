# Contributing

Ideas, bug reports and improvements to the method are welcome. By participating you agree to the [Code of Conduct](CODE_OF_CONDUCT.md). Vulnerabilities go through the private channel in [SECURITY.md](SECURITY.md), not through issues.

## Reporting a problem

Say which agent and version you used, what kind of app you audited (stack, roles), which phase went wrong, and what the agent did versus what the skill says. Remove any real data, URLs or credentials from what you paste.

## Before opening a pull request

There is no automated check yet. Until there is:

- Keep `SKILL.md` short: the method and the gates. Long material goes to `references/`.
- If you change the method, run the skill on a real app and say in the PR what you ran it on and what changed in the result.

## Repo rules

- **Simple stays simple.** No commands, hooks or bundled scripts unless an ADR says why ([ADR-0001](docs/adr/0001-ship-as-a-plain-skill.md)).
- **Never against production.** Any change that weakens isolation (isolated copy, test data) is rejected.
- **Report, don't implement.** The audit changes no product code; every proposal must stand alone in the report.
- **Measured, not felt.** A proposal without steps before and after is not a proposal.

## Versions

Don't bump the version by hand. Every push to `main` that touches `skills/` gets a patch bump in `.claude-plugin/plugin.json` from CI (`.github/workflows/bump-version.yml`), because `claude plugin update` only picks up a change when the version changes. For a minor or major bump, change it yourself in the same push: CI sees it and leaves it alone. CI commits to `main`, so pull before your next change.

## Commits and pull requests

One topic per pull request, a short imperative commit subject, and the reason in the body.
