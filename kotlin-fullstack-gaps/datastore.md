# DataStore

Этот файл нужен для app preferences, lightweight local state и migration away from SharedPreferences.

## Что пока не покрыто

- Preferences DataStore
- Proto DataStore
- schema decisions
- app settings flow
- migration strategy from SharedPreferences

## Что будущий skill должен уметь решать

- когда брать DataStore, а когда Room
- где хранить feature flags, theme, onboarding, auth-adjacent light state
- как проектировать typed settings models
- как expose settings through Flow cleanly

## Какие decision rules нужны

- DataStore для lightweight app or user preferences
- Room для relational or query-heavy data
- preference keys не должны торчать по всему приложению
- mapping from storage keys to domain-friendly settings model should be explicit

## Какие anti-patterns надо запретить

- random string keys all over the codebase
- UI directly reading DataStore internals
- storing complex relational state in preferences
- no migration plan when replacing SharedPreferences

## Минимальный reference pack на будущее

- preferences vs proto
- migration patterns
- settings repository examples
