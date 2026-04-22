# Dependency Injection

Use this reference for Hilt and dependency graph wiring.

## Hilt defaults

- prefer constructor injection
- use modules for external builders and interfaces that need binding
- scope deliberately

## Module rules

- group providers by ownership, not by random size
- keep networking providers together
- keep persistence providers together
- keep feature bindings near the feature when the project supports that

## Scope thinking

Think about lifecycle:

- application-wide singletons
- activity-retained or viewmodel-scoped objects
- short-lived unscoped objects

Do not mark everything singleton by habit.

## Review questions

- Does this class really need DI?
- Are dependencies minimal and explicit?
- Is the chosen scope correct for lifecycle and memory?
- Is the module doing wiring only, not business logic?
