# Testing

Use this reference for Kotlin tests, especially around business logic, coroutines, and Flow.

## Testing posture

- Test behavior that matters to callers.
- Prefer a few sharp tests over many noisy tests.
- Make the scenario easy to read.

## Unit tests

Good unit tests should:

- name the scenario clearly
- arrange only the state that matters
- assert the meaningful outcome

Avoid:

- asserting every internal step
- mocking value objects or simple pure functions
- brittle tests tightly coupled to implementation structure

## Coroutines

- Keep coroutine tests deterministic.
- Control timing rather than relying on sleeps.
- Assert cancellation and error behavior when relevant.

## Flow

- Assert the sequence of emissions that matters.
- Check initial state, updates, completion, and failure behavior where relevant.
- Avoid tests that merely collect without making the expected progression explicit.

## Boundary tests

Add integration-style tests when:

- serialization format matters
- persistence mapping matters
- Java interop or external APIs create risk
- concurrency boundaries affect correctness

## Review questions

- Does the test explain expected behavior?
- Is it resilient to harmless refactors?
- Are async behaviors deterministic?
- Is the boundary under test the right one?
