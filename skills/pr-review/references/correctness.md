# Correctness And Logic

Reconstruct the intended behavior from the PR description, repository conventions, callers, tests, and invariants. Then trace changed inputs through the affected paths to their observable results.

Look for:

- inverted conditions, missing branches, incorrect defaults, and error paths that silently succeed;
- changed state transitions that skip validation, cleanup, locking, rollback, or persistence;
- boundary cases such as empty input, duplicates, retries, timeouts, partial failure, concurrency, and permission changes;
- assumptions that hold for the changed test but fail for another real consumer;
- mismatches between names, documentation, types, and actual behavior;
- fixes that address a symptom while leaving the original failure path reachable.

Prefer a small reproducer, counterexample, failing test, or traced call path. Separate a proven defect from a question about intent.
