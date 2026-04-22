# Coroutines And Flow

Use this reference for async design, coroutine structure, cancellation, and Flow.

## Mental model

- `suspend` is for one asynchronous result
- `Flow` is for many values over time
- coroutine scope defines lifetime
- cancellation is part of correctness, not an optional bonus

## Choosing between `suspend` and `Flow`

Use `suspend` when:

- the work returns one result
- the caller asks once and gets one answer
- there is no meaningful stream semantics

Use `Flow` when:

- values change over time
- you need observation
- you combine multiple async sources
- the caller benefits from progressive updates

Do not use `Flow` for a single value just because the project uses coroutines.

## Structured concurrency

- Launch child work from a meaningful scope.
- Keep the lifecycle of work bounded by the owner.
- Avoid `GlobalScope`.
- Prefer explicit scope ownership.

## Cancellation

- Do not swallow cancellation accidentally.
- Avoid broad `catch (e: Exception)` unless cancellation is rethrown correctly.
- Keep long-running work cancellation-friendly.

## Dispatchers

- Be intentional about where blocking or CPU-heavy work runs.
- Keep UI/main-thread work light.
- Avoid hiding blocking I/O in code that appears cheap.

## Flow design

- Expose `Flow<T>` or `StateFlow<T>` publicly, not mutable variants.
- Use `StateFlow` for observable current state.
- Use `SharedFlow` for fan-out or event streams only when justified.
- Avoid event buses disguised as shared flows.

## Flow operators

- Prefer a small readable pipeline over a long clever one.
- Name intermediate values when a chain becomes mentally expensive.
- Be aware of concurrency and ordering behavior when using `flatMap*`, buffering, or sharing.

## Exceptions in coroutines and Flow

- Decide where exceptions become domain errors.
- Keep cancellation separate from ordinary failure handling.
- Do not let every collector invent its own error translation rules.

## Testing coroutines and Flow

- Use deterministic test dispatchers where available in the stack.
- Test emission sequences and terminal behavior.
- Prefer explicit assertions about state transitions.

## Review questions

- Should this be `suspend` instead of `Flow`?
- Who owns this scope?
- Does cancellation behave correctly?
- Is the public type immutable?
- Is the operator chain still readable?
