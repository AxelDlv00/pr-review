# Security And Trust Boundaries

Use this lens for changes involving authentication, authorization, untrusted input, subprocesses, network access, secrets, persistence, or user-controlled content.

Look for:

- authorization checks performed after a side effect, confused identity, or missing tenant/resource scope;
- injection, path traversal, unsafe deserialization, command execution, SSRF, or data exposure;
- secrets in logs, fixtures, diffs, error messages, or environment propagation;
- untrusted pull-request code being executed with repository, cloud, or host credentials;
- weakened validation, unsafe defaults, or missing rate and resource limits;
- security tests that validate only the happy path.

Require a concrete attack path and affected boundary for a blocker. If the threat depends on deployment or configuration evidence unavailable in the workspace, report the assumption and request human verification.
