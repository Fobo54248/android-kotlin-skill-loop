# testing integration

Этот файл нужен для стыка unit, integration, UI, and end-to-end testing in a real Kotlin product.

## Что пока не покрыто

- integration tests across layers
- contract tests
- UI instrumentation strategy
- end-to-end confidence for release-critical flows
- backend/mobile contract alignment

## Что будущий skill должен уметь решать

- какие тесты нужны на каком уровне
- где unit tests уже достаточно, а где нужен boundary verification
- как не заменять архитектурные тесты только UI tests
- как выбирать минимальный достаточный test pyramid

## Какие decision rules нужны

- business logic should mostly be proven below UI
- integration tests should target risky boundaries
- UI tests should validate behavior meaningful to users
- release-critical flows need stronger confidence than ordinary screens

## Какие anti-patterns надо запретить

- all confidence pushed into flaky UI tests
- no boundary tests for serialization or persistence
- duplicated assertions across layers with no extra signal

## Минимальный reference pack на будущее

- test pyramid for Kotlin app products
- contract and integration test patterns
- UI and E2E scope rules
