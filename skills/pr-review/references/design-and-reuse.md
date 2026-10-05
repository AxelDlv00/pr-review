# Design, Reuse, And Precedent

Review whether the change belongs at the right abstraction level and whether it builds on existing concepts instead of creating a competing local vocabulary.

Inspect analogous code in the same repository and its direct dependencies before searching elsewhere. Compare signatures, module boundaries, error behavior, naming, extension points, and ordinary call sites. Look for:

- duplicated near-clones that should share a general result;
- abstractions introduced for one caller that make a simple path harder to understand;
- APIs too specific to one fixture, product path, provider, or current implementation;
- helpers placed below the level where other consumers would naturally reuse them;
- public interfaces that expose implementation details or omit the operations users will need;
- a new framework or wrapper where a small local function or existing library facility is sufficient.

Give a concrete before/after example, an analogous declaration or implementation, and the benefit of the proposed choice. External examples are useful only when their source and applicability are stated. Do not invent claims about what developers regret or defend: use accepted code, migration notes, issue discussions, release notes, or clearly label the claim as a hypothesis for human judgment.
