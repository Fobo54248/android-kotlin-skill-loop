# Kotlin Multiplatform

Этот файл нужен, если под “fullstack Kotlin” мы реально хотим понимать shared code across Android and beyond.

## Что пока не покрыто

- commonMain ownership
- expect/actual design
- shared domain and data policies
- platform boundary leakage
- Compose Multiplatform considerations

## Что будущий skill должен уметь решать

- что должно жить в shared code, а что должно остаться platform-specific
- как не протащить Android assumptions into common code
- как проектировать shared domain, repositories, and platform adapters

## Какие decision rules нужны

- share logic only when it stays truly cross-platform
- platform APIs should be abstracted intentionally
- common code should not become a lowest-common-denominator junk drawer

## Какие anti-patterns надо запретить

- putting platform-specific assumptions in commonMain
- expect/actual overuse for things that should remain local
- forced sharing of UI or storage abstractions without payoff

## Минимальный reference pack на будущее

- shared boundary heuristics
- expect/actual guidance
- common vs platform layer patterns
