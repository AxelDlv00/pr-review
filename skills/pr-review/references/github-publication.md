# GitHub Publication

Publication is opt-in. Before writing, show or summarize the final content, confirm the repository, PR number, and exact head commit, and make sure the user explicitly requested posting.

The main agent performs every write through the authenticated GitHub integration or `gh`. Subagents return data only. Use a stable marker so rerunning the review updates the prior summary instead of creating an unbounded comment stream:

```html
<!-- pr-review:summary head=<full-head-sha> manifest=<manifest-id> -->
```

The summary issue comment should contain:

1. `## AI pre-review` and the exact head SHA;
2. the table from [reporting.md](reporting.md), with columns `rubric`, `state`, `judge`, and `summary`;
3. links or anchors for detailed findings;
4. checks run, limitations, and a statement that this is advisory human pre-review.

For a finding on a changed line, create a GitHub pull-request review comment with the exact head commit, file path, right-side line, severity, rubric, consequence, evidence, and requested change. Add a stable marker such as:

```html
<!-- pr-review:finding key=<stable-key> head=<full-head-sha> -->
```

Do not use a formal `APPROVE` or `REQUEST_CHANGES` review for this pre-review. Use ordinary comments so the human reviewer remains the decision-maker. Findings that cannot anchor to a changed line should remain in the summary comment with a file/symbol reference.

Manage only labels in the `pr-review:` namespace. Ensure these labels exist, remove stale labels in that namespace, and add the current aggregate state:

| Label | Meaning |
| --- | --- |
| `pr-review:in-progress` | A review is running for the current head. |
| `pr-review:approved` | Every selected rubric is green; this is not a merge approval. |
| `pr-review:changes-requested` | At least one rubric has an evidence-backed concern or blocker. |
| `pr-review:blocked` | A required rubric could not reach a trustworthy conclusion. |
| `pr-review:stale` | The reviewed head no longer matches the PR head. |
| `pr-review:error` | A rubric or publication step failed. |

Never remove or rewrite unrelated repository labels. If the head changes while publishing, stop and mark the result stale rather than attaching comments to a new revision.
