# Engineering Practices

Judge the change against the repository's language and framework conventions, then against broadly defensible engineering practice. This rubric is about decisions that affect future work, not personal formatting taste.

Look for:

- spaghetti control flow: deep nesting, hidden side effects, long functions, tangled state, or exception paths that cannot be followed locally;
- AI-shaped overproduction: long code or documentation that repeats obvious facts, wraps a small behavior in unnecessary layers, or adds speculative framework machinery;
- over-specific names, types, helpers, and configuration that encode one current example instead of the real contract;
- unclear ownership, inconsistent error handling, missing invariants, accidental global state, and APIs that make invalid use easy;
- poor dependency direction, weak separation of policy and mechanism, or tests coupled to incidental implementation;
- documentation that is misleading, too verbose for its audience, detached from the code, or missing the decisions a maintainer must know.

Do not equate line count with poor quality. Explain the cognitive, operational, or maintenance cost and show a smaller, clearer alternative when requesting change. For a non-obvious practice, cite a project-local precedent or a reliable external example and explain why it transfers.
