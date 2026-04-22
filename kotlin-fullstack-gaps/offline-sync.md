# Offline And Sync

Этот файл нужен для offline-first поведения, cache policy и reconciliation between local and remote state.

## Что пока не покрыто

- offline-first screens
- sync strategies
- stale data policy
- optimistic updates
- conflict handling

## Что будущий skill должен уметь решать

- когда local-first оправдан
- где описывать freshness policy
- как показывать stale content, refresh, and failure states
- как проектировать sync without duplicating logic everywhere

## Какие decision rules нужны

- cache policy должна быть названа и понятна
- refresh-on-open and offline-first are different product behaviors
- optimistic update requires rollback or reconciliation thinking
- repository should own merge policy

## Какие anti-patterns надо запретить

- implicit cache behavior
- same screen treating stale and fresh data identically when product meaning differs
- optimistic updates without error path
- sync logic duplicated in multiple ViewModels

## Минимальный reference pack на будущее

- cache policy catalog
- stale content UI patterns
- optimistic update patterns
- merge and reconciliation rules
