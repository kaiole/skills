---
name: cpp
description: Design, implement, debug, and review C++ with attention to ownership, contracts, and verification. Use when writing or changing C++ code, starting a C++ project, or assessing a C++ change in an existing codebase.
---

# C++

Make focused, idiomatic changes that fit the project. Prefer clear ownership,
simple designs, and evidence over a universal toolchain or style.

## Discover before editing

- Read applicable project instructions, the affected code, callers, and tests.
  Find the supported C++ standard, compilers/platforms, dependencies, build and
  CI commands, formatting/lint rules, and relevant verification workflows.
- Establish local conventions, ownership/lifetime assumptions, and the error
  model, including whether exceptions are enabled. Follow reasonable patterns;
  flag unsafe ones rather than copying them or redesigning the project unasked.
- Identify the intended behavior and actual contracts from requirements,
  documentation, and usage, including complexity and compatibility constraints.
  Resemblance to a standard-library type does not imply its entire contract.
- Run relevant existing checks before changing code where feasible. Record
  pre-existing failures or unavailable checks so regressions remain distinguishable.
- For a new project or incomplete tooling, clarify material unknowns and propose
  minimal appropriate setup for human approval. Do not silently install a stack
  or impose a build system, C++ version, naming style, or error policy. Keep
  setup changes separate from feature work where feasible.

## Design proportionally

- Prefer value semantics, standard-library facilities, and the simplest design
  that meets the requirements within the supported language/library version.
  Add abstractions, templates, inheritance, or dependencies for a concrete need,
  not hypothetical reuse. Avoid unrelated cleanup.
- Use types to express meaningful invariants and validate external input at
  boundaries. Choose representations and error reporting for the domain and
  project; do not mandate a particular sum type or exceptions-versus-status rule.
  Do not silently discard failures or turn them into plausible default values.
- Preserve existing behavior and documented contracts unless the task requires
  changing them. Make intended changes and compatibility consequences explicit.
- Treat performance constraints as requirements to establish, not defaults.
  Do not universally ban allocation, locking, exceptions, or virtual dispatch.
  Justify performance-driven complexity with representative measurements or a
  concrete resource/timing contract; keep setup work outside hot paths as needed.

## Ownership and correctness

- Use RAII for resources and prefer the rule of zero. Make ownership explicit:
  prefer values or unique ownership; use shared ownership only when genuinely
  needed. Make legacy/raw ownership boundaries clear rather than assuming them.
- Non-owning pointers, references, iterators, spans, and views must not outlive
  their referents. Check temporaries, captures, asynchronous work, and stored
  views where relevant. Understand which mutations invalidate each kind of view;
  do not assume every mutation invalidates everything.
- When managing resources manually, consider copy/move/destruction together,
  including self-assignment, moved-from validity, and partial construction.
  Use `noexcept` only when its guarantee is valid, including called operations;
  never add it merely to suppress exceptions or force move optimizations.
- For affected operations, reason about self-aliasing, overlapping input,
  iterator/reference invalidation, and failure partway through mutation.
  Preserve the required exception guarantee; do not promise a strong guarantee
  universally. Release resources and leave state consistent on failure.
- Check arithmetic bounds, signed overflow, mixed signedness, narrowing,
  alignment, object lifetime, and aliasing rules when relevant. A cast is not
  proof of safety. Byte copying is not a general relocation mechanism.
- For shared mutable state, establish synchronization and lifetime rules.
  Consider data races, lock ordering, and shutdown; do not assume atomics alone
  make a protocol correct.

## Verify and hand off

- Add appropriate public-behavior regression, boundary, and error-path tests.
  For a bug, reproduce it and demonstrate the regression test fails before the
  fix where feasible. Select edges from the contract, not a rote checklist.
- Derive expected results independently from requirements, hand calculations,
  or a trusted oracle—not by recording the implementation's output as truth.
- Run existing relevant builds, tests, formatting, lint/static analysis, and
  feature checks. Use sanitizer and optimized configurations where available
  and appropriate; match additional checks to the risk and supported platforms.
  Inspect actual output and ensure the intended tests ran, not just an exit code.
- Do not weaken checks or tests to manufacture success. Legitimate test updates
  for changed requirements and narrow, justified suppressions need an explanation
  and must preserve meaningful coverage. Separate unrelated baseline failures.
- Review the diff for scope, contracts, lifetime hazards, and missing behavior.
  Passing checks are evidence, not proof of sound design or completeness.
- Leave changes for human review. Briefly report changes, important decisions,
  commands and outcomes, pre-existing failures, and missing or unrun checks with
  reasons. State remaining uncertainty rather than claiming unverified success.
