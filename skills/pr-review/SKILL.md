---
name: pr-review
description: Orchestrate a structured, evidence-first pre-review of a GitHub pull request or current branch before human review. Dispatch focused rubric subagents, adjudicate their findings, and publish a summary table, rubric details, inline findings, and visibility labels for GitHub PRs. Do not merge or push.
---

# Pull Request Pre-Review

This is a pre-review for a human engineer. Its purpose is to find plausible defects and make the later human review faster. It is not an approval, merge decision, or substitute for repository maintainers.

## Inputs

Accept a pull request URL or number, or infer the current branch and its merge base when the user asks to review the current changes. Ask for the repository or target branch only when they cannot be determined from the workspace or request.

Before reviewing, establish:

- repository and target branch;
- exact base and head commit IDs;
- changed files and the effective diff;
- repository instructions, supported toolchain, and relevant tests;
- the user's requested lenses, if any.

If the head changes during the review, state that the result is stale and identify the commit that was actually reviewed.

## Review workflow

1. Read the repository's contributor instructions and inspect the complete diff. Follow local instructions before running commands.
2. Create an immutable review manifest containing repository, base commit, head commit, selected rubric revisions, agent/model, and checks to run. Never mix findings from different heads; a rerun gets a new manifest.
3. Classify the change and select relevant rubrics. Dispatch one independent, read-only subagent per selected rubric when native subagents are available. Core rubrics are correctness, compatibility, generality, design and reuse, and maintainability. Add engineering practices, testing and operations, security, performance, or documentation and scope when relevant.
4. Give every subagent the exact manifest, narrow rubric scope, repository instructions, and a structured return contract. Subagents do not edit files, approve, merge, or push. They return a result that the main agent publishes as that rubric's detail comment.
5. Inspect surrounding code and real consumers. A diff-only argument is insufficient for claims about behavior, compatibility, public API, concurrency, persistence, or security.
6. Run focused checks and tests where practical. Treat a passing test as evidence about that test's scope, not proof that the change is correct.
7. Adjudicate every returned finding. Keep it only when the evidence supports a concrete consequence, downgrade unsupported claims to reviewer focus, and deduplicate findings that describe the same failure. A clean result is valid.
8. Report findings using [references/reporting.md](references/reporting.md). For a GitHub PR input, publish the summary, one detail comment per selected rubric, anchored finding comments, and aggregate labels by default through [references/github-publication.md](references/github-publication.md). Only suppress publication when the user says `local`, `dry-run`, or equivalent.

Read only the relevant lens references:

- [correctness.md](references/correctness.md) for behavior, invariants, and logical errors.
- [compatibility.md](references/compatibility.md) for public APIs, data, wire formats, and upgrades.
- [quality.md](references/quality.md) for design, maintainability, and repository fit.
- [design-and-reuse.md](references/design-and-reuse.md) for abstractions, precedent, and concrete analogies.
- [generality.md](references/generality.md) for future compatibility, useful generality, and over-specialization.
- [practices.md](references/practices.md) for engineering conventions and defensible implementation choices.
- [testing.md](references/testing.md) for tests, observability, operations, and performance.
- [scope-and-docs.md](references/scope-and-docs.md) for PR boundaries, documentation, and examples.
- [security.md](references/security.md) for trust boundaries, secrets, and unsafe execution.
- [subagents.md](references/subagents.md) when delegating independent review passes.

## Boundaries

Keep the workspace unchanged unless the user explicitly asks for a repair. Do not silently rewrite code to make a finding true. Do not report formatting preferences as defects. Do not request changes merely because an alternative design is imaginable.

Do not approve or merge. For a GitHub PR, publication is part of the normal pre-review: the main agent posts ordinary comments and manages only `pr-review:*` labels after verifying the reviewed head. A `local` or `dry-run` request suppresses all GitHub writes. The main agent owns all writes so the summary and rubric comments remain idempotent; each comment identifies the subagent judge that produced it.

## Review result

Start with the reviewed repository and commit IDs, the checks actually run, and any limitations. Then list the rubric table and findings with precise file and line locations. End with a short reviewer-focus section for issues that require human judgment but are not demonstrated defects.
