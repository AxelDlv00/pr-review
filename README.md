# PR Pre-Review Plugin

This is an independent, skills-only plugin for Codex and compatible agent environments. It gives a main agent a repeatable, evidence-first workflow for reviewing a pull request before a human review. The main agent dispatches focused rubric subagents, adjudicates their findings, and can publish a Tau Ceti-style summary table, inline details, and `pr-review:*` labels. It does not contain a server, GitHub Action, or CLI.

## Use

Install the plugin in the agent environment, then explicitly invoke the skill:

```text
$pr-review https://github.com/owner/repository/pull/42
```

In Codex, skills can also be selected through `/skills`. Ask for additional lenses in the same prompt, for example `Focus on backward compatibility and migration safety.`

The skill is read-only by default. It reports findings in the session and does not publish GitHub comments, labels, push changes, or merge a pull request without a separate explicit request. When publishing is requested, only the main agent writes to GitHub and it pins every write to the reviewed head commit.

## Contents

- `skills/pr-review/SKILL.md`: the review workflow and boundaries.
- `skills/pr-review/references/`: focused review lenses, subagent contract, reporting contract, and GitHub publication protocol.
- `skills/pr-review/agents/openai.yaml`: Codex display metadata and explicit-only invocation.

The rubrics are provider-neutral. The orchestrator can use Codex, Claude, or another host's native subagents for independent review passes when available. Reviewers are advisory and never replace human ownership of the merge decision.

## License

Apache-2.0.
