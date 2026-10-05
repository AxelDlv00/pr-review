# Reporting Contract

The report is advisory. It must let a human reproduce the reasoning without trusting the model's conclusion. The main agent is the adjudicator; a subagent's proposed state is evidence, not an automatic verdict.

## Rubric result

Each selected rubric returns one result with:

- `rubric`: stable lowercase rubric name;
- `state`: `approved`, `changes_requested`, `blocked`, `error`, or `stale`;
- `judge`: provider/model and, when useful, the subagent role;
- `summary`: one or two sentences suitable for the PR summary table;
- `findings`: zero or more findings using the contract below;
- `coverage`: files, symbols, checks, and assumptions inspected;
- `limitations`: missing evidence or unresolved questions.

The main agent may change `state` after adjudication, but it must preserve the subagent result and explain a disagreement in the review record.

For the GitHub summary, render one row per rubric in this exact shape:

```markdown
| rubric | state | judge | summary |
| --- | --- | --- | --- |
| correctness | ✅ approved | codex/gpt-6 | No demonstrated behavioral defect found. |
| compatibility | 🟡 changes requested | claude/opus | Existing configuration readers reject the new field shape. |
```

Use `✅` for approved, `🟡` for changes requested, `🔴` for blocked, `⚠️` for error, and `⏳` for in progress. Use `🕒` for stale evidence. The summary is advisory; even an all-green table does not replace human review.

For each finding, include:

- `severity`: `blocker`, `concern`, or `suggestion`;
- `confidence`: high, medium, or low;
- `lens`: the review perspective that found it;
- `location`: file and line, or the smallest relevant symbol/range;
- `finding`: the concrete behavior or defect;
- `consequence`: what can break and for whom;
- `evidence`: the code path, consumer, test, command, or observation supporting it;
- `requested_change`: a bounded correction or decision;
- `verification`: a test or inspection that would confirm the correction, when useful.

Use `blocker` only for a demonstrated correctness, security, data-loss, compatibility, or release failure. Use `concern` when the risk is material but evidence is incomplete or the impact depends on an unresolved assumption. Use `suggestion` for a concrete improvement with a demonstrated benefit. Do not invent a finding to fill a lens.

Recommended shape:

```markdown
## Findings

### [blocker] Public parser accepts invalid state
- Lens: compatibility
- Location: `src/parser.py:117`
- Confidence: high
- Finding: ...
- Consequence: ...
- Evidence: ...
- Requested change: ...
- Verification: ...

## Reviewer focus

- An unresolved design question that needs a human decision.

## Coverage and limits

- Lenses used, commands run, reviewed base/head, and unavailable evidence.
```

When no supported finding remains, say so plainly and summarize what was inspected. Do not call the change safe or fully correct.
