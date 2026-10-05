# Tests, Performance, And Operations

Check whether the tests and operational evidence cover the risk introduced by the change. Inspect existing test conventions and run focused checks when the environment permits.

Look for:

- missing tests for changed branches, failure paths, boundaries, and regression scenarios;
- tests that assert implementation details while missing the user-visible contract;
- nondeterminism, flaky timing, order dependence, leaked resources, or tests that do not actually exercise the changed path;
- unbounded work, accidental quadratic behavior, excess network or database calls, and memory growth;
- missing metrics, logs, alarms, migration visibility, or rollback signals for operationally significant changes;
- checks that pass only because errors are swallowed, fixtures are unrealistic, or the command did not cover the changed target.

Report a missing test as a concern or suggestion unless the absent check leaves a demonstrated release or correctness failure.
