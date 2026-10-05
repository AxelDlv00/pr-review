# Independent Review Passes

The main reviewer is the orchestrator. It should dispatch one subagent per selected rubric when native subagents are available. Do not create duplicate subagents for the same rubric merely to multiply output; a second model is useful only when the main agent explicitly wants cross-model disagreement or verification.

Give every reviewer this context:

```text
You are the <rubric> reviewer in a read-only pre-review of repository <repository> at head <head> against base <base>.
Review only the supplied scope through the <lens> rubric. Read repository instructions and inspect relevant consumers.
Do not edit files, publish comments or labels, approve, merge, or request changes on GitHub.
Return exactly one rubric result containing rubric, state, judge, summary, findings, coverage, and limitations. The judge must identify the provider, exact model, reasoning effort, rubric role, and native subagent ID when available. Return an explicit approved result when no supported finding remains. Findings must include severity, confidence, location, consequence, evidence, requested change, and verification.
```

Useful roles are:

- correctness reviewer: changed behavior, invariants, edge cases, state transitions, and error paths;
- compatibility reviewer: public APIs, serialized data, migrations, dependency/toolchain changes, and old consumers;
- quality reviewer: module boundaries, maintainability, naming, ownership, repository conventions, overlong AI-shaped code or documentation, spaghetti control flow, and unjustified specificity;
- generality reviewer: future compatibility, extension points, reusable abstractions, migration risk, and whether a narrower implementation unnecessarily hardens today's details into tomorrow's API;
- test and operations reviewer: regression coverage, failure paths, resource use, observability, and rollout concerns;
- security reviewer: authorization, untrusted input, secrets, subprocesses, network boundaries, and data exposure.

The parent agent owns integration and publication. It must inspect the reviewers' evidence, remove duplicate findings, downgrade unsupported claims, and preserve disagreements as explicit reviewer-focus questions when they cannot be settled from the repository. A finding intended for an inline comment must identify an exact changed-file path, line, side, and head commit; otherwise it belongs in the summary or reviewer-focus section.
