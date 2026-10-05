# Generality And Future Compatibility

Assess whether the implementation will remain useful as the project, users, providers, and data evolve. This is broader than checking today's backward compatibility: it asks whether the PR unnecessarily turns a temporary detail into a public contract.

Inspect:

- APIs, schemas, configuration, event formats, and extension points for assumptions that make the next compatible feature difficult;
- code specialized to one provider, model, backend, platform, fixture, tenant, or current call site when the surrounding concept is broader;
- abstractions that are too narrow to reuse, or abstractions that are too broad and speculative to justify their cost;
- one-off branches and wrappers that would multiply when a second implementation or consumer arrives;
- defaults, names, and exported types that make future migration or deprecation harder;
- whether the code could support the stated problem with a smaller general mechanism rather than a growing set of special cases.

Require a concrete future scenario, affected contract, or analogous implementation before requesting a generalization. Show a bounded alternative: a parameter, interface, data shape, shared helper, or clearer seam. Do not demand maximal abstraction or hypothetical configurability.

For provider-specific code, explicitly ask whether the surrounding workflow claims to be provider-neutral. A Codex-only choice is a finding when the public contract presents a general agent workflow and the specialization creates avoidable lock-in; it is acceptable when the repository deliberately declares Codex as its scope or the provider-specific capability is essential.

Use accepted code in comparable projects, migration notes, issue discussions, or official APIs as evidence for choices developers defend or later regret. Do not present generic folklore as evidence.
