# Compatibility And Public Contracts

Inspect callers, consumers, serialized data, CLI usage, configuration, migrations, and documented interfaces. Compare the new behavior with the previous revision and identify the users who rely on the old contract.

Look for:

- removed or narrowed APIs, changed defaults, renamed fields, and altered error behavior;
- wire, file, database, cache, or event formats that cannot read existing data or interoperate with older versions;
- migrations without downgrade, backfill, rollout, or mixed-version reasoning where those are required;
- changed ordering, timing, idempotency, or retry behavior that breaks clients;
- dependency or toolchain changes that exceed the stated scope;
- tests that cover only the new path and fail to exercise old callers or compatibility boundaries.

Do not demand compatibility with an explicitly documented breaking change. State the affected contract and the smallest evidence-backed mitigation.
