# ADR-0001: Ship as a plain skill, packaged only for installation

- **Status:** accepted
- **Date:** 2026-11-09

## Context

The method was first run by hand in one session, on a restaurant point-of-sale SaaS. It worked because the agent followed a clear sequence (interview, spec, isolated walkthrough, report, small fixes with tests) using tools it already had: a browser driver, git worktrees and the project's own test suite.

The owner wants it reusable across many repositories, and explicitly simple: "like any skill, otherwise it turns into a plugin".

## Decision

The deliverable is one `SKILL.md` plus a `references/` folder, following the open Agent Skills format. A minimal `.claude-plugin/` (`plugin.json` + `marketplace.json`) is added only so it installs with `claude plugin install`; it adds no commands, hooks, agents or scripts of its own.

## Alternatives considered

| Alternative | Why it was rejected |
|---|---|
| Full plugin with slash commands, hooks and subagents | The owner asked for a simple skill; extra moving parts would need maintenance in every repo that installs it |
| Bundled scripts (seeders, crawlers) | Each project's stack is different; the agent writes the small per-project snippets the references describe |
| A prompt kept in a notes file | Not installable, not versioned, easy to drift between repos |

## Consequences

- The skill depends on tools the host agent already has (a browser automation tool, git, the project's test runner). The `SKILL.md` must say what to do when one is missing.
- Improvements happen in one place and reach every repo on update.
- Measurements live as short snippets in `references/`, not as maintained code.

## Sources

- [Claude Code: Agent Skills](https://code.claude.com/docs/en/skills)
- [Claude Code: Plugin marketplaces](https://code.claude.com/docs/en/plugin-marketplaces)
- [Agent Skills specification](https://agentskills.io/specification)
