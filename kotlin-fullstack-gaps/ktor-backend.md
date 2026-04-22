# Ktor Backend

Этот файл нужен, если fullstack Kotlin skill должен действительно включать backend, а не только Android app code.

## Что пока не покрыто

- Ktor server structure
- routing and modules
- serialization on backend
- request validation
- auth boundaries
- data access and service layers
- API error contracts

## Что будущий skill должен уметь решать

- как строить Kotlin backend idiomatically
- как разделять transport, service, domain, and persistence layers
- как держать API contracts stable
- как проектировать errors and validation cleanly

## Какие decision rules нужны

- Ktor backend should stay Kotlin-idiomatic, not Java web shaped
- route handlers should stay thin
- business logic should not live in raw route blocks
- transport models and domain models should not blur accidentally

## Какие anti-patterns надо запретить

- fat routing files
- database access directly in handlers
- no clear validation boundary
- leaking internal exception shapes to clients

## Минимальный reference pack на будущее

- route/module structure
- validation and error mapping
- service vs repository boundaries
