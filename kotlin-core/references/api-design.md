# API Design

Use this reference for public surfaces, class design, type modeling, and error strategy.

## Public API principles

- Make the easy path the safe path.
- Minimize ambiguity in names and nullability.
- Prefer fewer concepts with clearer contracts.
- Hide implementation detail unless extension is a real requirement.

## Functions

- Prefer names that describe meaning, not mechanism.
- Avoid overload sets that are hard to distinguish.
- Avoid boolean parameters in public APIs when named alternatives or sealed options are clearer.
- Prefer return values that explain outcome.

## Type modeling

- Use `data class` for immutable value carriers.
- Use sealed hierarchies for closed outcome or state sets.
- Use enums for simple closed labels without payloads.
- Use value objects to give names to important primitives.

## Interfaces

Use an interface when:

- multiple implementations are genuinely expected
- mocking or substitution is an actual need in the architecture
- the abstraction expresses a stable boundary

Do not create interfaces just because code “might need them later”.

## Extension functions

Use extensions when:

- the operation is naturally phrased on the receiver
- discoverability improves
- the behavior does not surprise readers

Do not use extensions to hide unrelated dependencies or create pseudo-method soup.

## Errors and results

Choose one dominant style per boundary:

- exceptions for exceptional failures
- nullable return for simple absence
- `Result` or sealed outcomes for expected branching

Document the contract through the type system whenever possible.

## Encapsulation

- Expose the smallest API needed.
- Prefer `private` and `internal` by default where appropriate.
- Avoid mutable state leaking through getters or public properties.

## Review questions

- Is the API obvious to call correctly?
- Do names match behavior?
- Are the types carrying the real meaning?
- Is this abstraction justified?
