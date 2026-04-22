---
name: kotlin-core
description: Use when working with general Kotlin code and needing detailed guidance for implementing, reviewing, debugging, refactoring, or explaining idiomatic Kotlin. Apply this skill for Kotlin language fundamentals, coding conventions, null safety, data and sealed models, collections, extension functions, coroutines, Flow, serialization, testing, Java interop, and API design across backend, Android, CLI, and library codebases.
---

# kotlin-core

Use this skill for Kotlin-first work where the main challenge is writing good Kotlin rather than using one specific framework.

This skill is the general-purpose foundation for:

- backend Kotlin
- Android Kotlin that is not deeply framework-specific
- CLI tools
- shared libraries
- Kotlin Multiplatform common code
- code review and refactoring of existing Kotlin projects

## What this skill optimizes for

- idiomatic Kotlin over Java-shaped Kotlin
- clear null-safety and predictable types
- readable, maintainable code with strong defaults
- small public APIs with explicit behavior
- structured concurrency and correct Flow usage
- incremental improvements that fit the existing codebase

## What this skill does not cover deeply

This skill is intentionally general. For framework-heavy work, combine it with a specialized skill when available.

Use a specialized skill for framework-heavy work when one exists. If no specialization exists, use this skill as the language-level source of truth and preserve the project's current framework patterns.

## Core workflow

### Step 0: Identify the Kotlin context

Determine which kind of Kotlin project you are in:

- JVM backend
- Android app
- library or SDK
- CLI/tooling
- Kotlin Multiplatform
- mixed Kotlin/Java codebase

Inspect before changing code:

- Gradle setup: `build.gradle.kts`, `settings.gradle.kts`, version catalogs
- Kotlin version and plugin usage
- module boundaries
- test stack
- serialization stack
- concurrency model
- framework dependencies

Do not assume coroutines, Flow, serialization, DI, or testing conventions. Inspect first.

### Step 1: Match the codebase before improving it

Read surrounding files and match:

- package naming
- file organization
- naming conventions
- visibility choices
- result/error patterns
- whether the project prefers classes, interfaces, sealed types, or plain functions
- whether the project already uses `Result`, custom error models, or exceptions

Improve code toward idiomatic Kotlin, but do not force a style rewrite that conflicts with the rest of the repository unless the user explicitly wants that.

### Step 2: Classify the task

Route the work into one or more of these modes:

- implementation
- refactor
- debugging
- code review
- API design
- migration from Java-style Kotlin
- concurrency cleanup
- serialization/model cleanup
- test hardening

Then apply the relevant rules from the references.

### Step 3: Apply Kotlin-first design choices

Default preferences:

- prefer `val` over `var`
- prefer expressions when they stay readable
- prefer non-null types by default
- prefer total and explicit state modeling
- prefer `data class` for pure state holders
- prefer `sealed interface` or `sealed class` for closed result/state hierarchies
- prefer top-level functions for stateless helpers when local ownership is clear
- prefer constructor injection where dependencies exist
- prefer small functions over deep inheritance

### Step 4: Verify behavior and maintainability

Check:

- nullability is explicit and justified
- types express intent clearly
- concurrency respects cancellation
- Flow usage reflects real streaming needs
- serialization models are isolated from domain logic when appropriate
- public API names are stable and understandable
- tests cover changed behavior

### Step 5: Explain tradeoffs briefly

When there are multiple valid Kotlin approaches, explain the chosen one briefly and in outcome terms:

- readability
- safety
- consistency with the codebase
- API stability
- performance or allocation impact if relevant

## Default Kotlin rules

### General language posture

- Write Kotlin as Kotlin, not as Java with different syntax.
- Avoid needless ceremony.
- Keep state and behavior close when it improves comprehension.
- Prefer explicit modeling over comments that explain ambiguous code.
- Use language features to reduce accidental complexity, not to look clever.

### Mutability

- Default to immutable references and immutable data flow.
- Introduce `var` only when mutation is real and useful.
- If mutation exists, keep its scope narrow and obvious.

### Nullability

- Model nullability deliberately, not lazily.
- Avoid `!!` unless the invariant is extremely clear and local.
- Prefer safe calls, Elvis, early returns, and explicit branching.
- Avoid leaking platform types across boundaries without normalization.

Read `references/null-safety.md` for detailed rules.

### Functions

- Keep functions focused on one meaningful responsibility.
- Prefer names that describe effect or returned meaning.
- Avoid boolean flag parameters when a sealed type or separate function is clearer.
- Prefer returning meaningful values over mutating outer state.
- Use extension functions only when they improve discoverability and read naturally.

### Classes and types

- Use `data class` for immutable state containers.
- Use value objects when primitive obsession hurts clarity.
- Use sealed hierarchies when state or outcomes are closed and meaningful.
- Avoid interfaces with one implementation unless they serve a real architectural need.
- Avoid inheritance when composition is simpler.

Read `references/api-design.md` for detailed guidance.

### Collections and transformations

- Prefer standard library collection operations over manual loops when readability improves.
- Avoid chaining too many transformations if it obscures the flow.
- Use sequences only when laziness materially helps.
- Prefer named intermediate values over unreadable fluent pipelines.

### Error handling

- Keep one clear error strategy per boundary.
- Use exceptions for exceptional failures when the surrounding codebase already does.
- Use typed results or sealed outcomes when failure is part of normal control flow.
- Do not mix exception-heavy and result-heavy styles arbitrarily in the same layer.

### Coroutines and Flow

- Prefer `suspend` for one-shot async work.
- Prefer `Flow` for streams, observation, or progressive updates.
- Prefer structured concurrency.
- Avoid `GlobalScope`.
- Respect cancellation and dispatcher boundaries.
- Avoid exposing mutable flow types publicly.

Read `references/coroutines-flow.md` for detailed rules.

### Serialization

- Keep wire format concerns in transport models when possible.
- Do not spread serialization annotations across domain models without a reason.
- Preserve backward compatibility intentionally when formats are external or persisted.

Read `references/serialization.md` for detailed rules.

### Testing

- Test behavior, not implementation noise.
- Prefer focused unit tests for business logic.
- Add integration tests where boundaries matter.
- Make coroutine and Flow tests deterministic.

Read `references/testing.md` for detailed rules.

## Review checklist

When reviewing Kotlin code, look for:

- Java-shaped patterns that Kotlin can simplify
- nullable values that should not be nullable
- misuse of `!!`
- overuse of scope functions causing ambiguity
- large functions mixing mapping, branching, and side effects
- public APIs with unclear contracts
- excessive interfaces or indirection
- coroutine scope misuse
- Flow used where a suspend function would be simpler
- serialization concerns leaking into business logic
- tests that mirror implementation rather than behavior

## Anti-patterns to avoid

- using `!!` as a routine escape hatch
- exposing mutable collections or mutable flow types publicly
- hiding important control flow inside nested `let` / `also` / `apply`
- creating abstractions before a second real use case exists
- writing one-line code that is harder to read than a short block
- leaking Java platform types across Kotlin APIs
- using coroutines where synchronous code is simpler and sufficient
- using Flow for single values
- mixing transport, persistence, and domain models without intent

## Reference map

Read only what is relevant:

- `references/style.md` for Kotlin coding style, file organization, and idiomatic structure
- `references/null-safety.md` for nullable types, platform types, and `!!` avoidance
- `references/coroutines-flow.md` for `suspend`, coroutine scopes, cancellation, and Flow
- `references/api-design.md` for public API shape, classes, sealed types, and error design
- `references/serialization.md` for DTOs, serialization boundaries, and schema evolution
- `references/testing.md` for unit tests, coroutine tests, and Flow verification

## Output expectations

- Make the smallest clean change that solves the task.
- Prefer code that a Kotlin team would keep, not tutorial code.
- If the repository style conflicts with ideal Kotlin style, move it in a better direction incrementally.
- When uncertain between two valid patterns, choose the one that reduces future confusion.
