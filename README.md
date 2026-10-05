# PR Pre-Review Plugin

This is an independent, skills-only plugin for Codex and compatible agent environments. It gives a main agent a repeatable, evidence-first workflow for reviewing a pull request before a human review. The main agent dispatches focused rubric subagents, adjudicates their findings, and publishes a Tau Ceti-style summary table, one detail comment per rubric, inline findings, and `pr-review:*` labels for a GitHub PR. It does not contain a server, GitHub Action, or CLI.

## Use

Install the plugin in the agent environment, then explicitly invoke the skill:

```text
$pr-review https://github.com/owner/repository/pull/42
```

In Codex, skills can also be selected through `/skills`. Ask for additional lenses in the same prompt, for example `Focus on backward compatibility and migration safety.`

The skill publishes comments and labels by default when invoked with a GitHub PR. Say `local` or `dry-run` to keep the result in the session. It never pushes changes, approves, or merges. Only the main agent writes to GitHub, and every write is pinned to the reviewed head commit.

## Contents

- `skills/pr-review/SKILL.md`: the review workflow and boundaries.
- `skills/pr-review/references/`: focused review lenses, subagent contract, reporting contract, generality guidance, and GitHub publication protocol.
- `skills/pr-review/agents/openai.yaml`: Codex display metadata and explicit-only invocation.

The rubrics are provider-neutral. The orchestrator can use Codex, Claude, or another host's native subagents for independent review passes when available. Reviewers are advisory and never replace human ownership of the merge decision.

## License

Apache-2.0.
