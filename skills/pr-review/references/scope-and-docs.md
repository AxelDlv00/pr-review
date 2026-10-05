# Documentation And Scope

Use this rubric when a PR changes documentation, public examples, release notes, migration guidance, or a broad set of files.

Check that:

- the stated problem and actual diff agree;
- the PR has one coherent purpose and does not hide unrelated cleanup or generated output;
- documentation describes observable behavior, supported commands, failure modes, and compatibility boundaries accurately;
- examples compile or run when the repository treats them as executable guidance;
- long explanations add decisions, constraints, or rationale rather than restating the implementation;
- public docs do not promise support, performance, security, or generality that the code does not provide.

Prefer a bounded split or a precise correction. Do not request a shorter document merely because it is long; identify repetition, missing structure, or a concrete reader failure.
