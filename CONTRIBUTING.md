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
- **Never against production.** Any change that weakens isolation (own worktree, isolated copy, test data) is rejected.
- **Fixes must be verified.** The "test seen failing against the old code" rule is part of the method, not a suggestion.

## Commits and pull requests

One topic per pull request, a short imperative commit subject, and the reason in the body.
