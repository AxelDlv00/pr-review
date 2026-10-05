# Design And Code Quality

Assess the change as part of the repository, not as an isolated patch. Read the relevant architecture and contributor guidance before judging structure.

Look for:

- duplicated logic that can drift, unclear ownership, and abstractions that obscure rather than simplify;
- dependency direction or module boundaries that make future changes or testing harder;
- public names, types, and interfaces that make ordinary use error-prone;
- resource lifetime, error propagation, logging, and configuration patterns inconsistent with the codebase;
- dead paths, accidental generated files, or undocumented behavior introduced by the change;
- complexity or cleverness with a concrete maintenance cost.

Treat style preferences as suggestions. A quality finding should identify a concrete future failure, user cost, or substantial maintenance burden.
