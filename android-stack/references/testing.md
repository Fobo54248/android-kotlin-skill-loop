# Testing

Use this reference for Android architecture testing across layers.

## What to test

Prefer tests for:

- mapping rules
- repository behavior
- use case logic
- ViewModel state transitions
- serialization or persistence boundaries that can break silently

## Compose tests

Add UI tests when:

- interaction behavior is important
- accessibility semantics matter
- state rendering has meaningful branches

Do not use UI tests to cover business logic that belongs below the UI layer.

## Repository tests

Repository tests should validate:

- local vs remote selection behavior
- mapping correctness
- cache or refresh policy
- error translation

## ViewModel tests

ViewModel tests should validate:

- initial state
- loading transitions
- success state
- error state
- one-time event behavior

## General rule

Test the boundary where behavior becomes meaningful to the next layer.
