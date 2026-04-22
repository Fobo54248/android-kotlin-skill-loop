# Kotlin Style

Use this reference for code style, organization, naming, and idiomatic expression.

## Source of truth

Base style decisions on Kotlin official coding conventions:

- file naming should follow the primary declaration or purpose of the file
- top-level declarations are normal in Kotlin
- class and file organization should optimize discoverability and readability
- naming should be predictable and boring

## Style rules

- Prefer the standard Kotlin formatting and organization used by IntelliJ or Android Studio.
- Keep related declarations near each other.
- Avoid giant utility files.
- Prefer one meaningful public type per file when that improves navigation.
- Use expression bodies when they are short and improve clarity.
- Use block bodies when logic or branching is non-trivial.

## Naming

- Classes, interfaces, and objects: nouns or noun phrases
- Functions: verbs or verb phrases
- Boolean properties and methods: names that read naturally as truth values
- Constants: use `UPPER_SNAKE_CASE` only for true constants
- Avoid meaningless suffixes like `Helper`, `Manager`, `Processor` unless they describe a real role

## Scope functions

Use scope functions deliberately:

- `let` for null handling or scoped transformation
- `run` for computing a result from a receiver
- `apply` for object configuration
- `also` for side effects that should not change the value
- `with` for batching receiver access when it improves readability

Avoid nested scope functions when the current receiver becomes unclear.

## Idiomatic simplifications

Prefer:

- `when` over long `if/else if` chains when selecting among multiple cases
- smart casts over manual type variables where possible
- destructuring only when it improves readability
- standard library functions before custom helpers

Avoid:

- overly clever operator overloading
- compressed chaining that hides intent
- large files full of unrelated extension functions

## File organization

Common good order inside a Kotlin file:

1. package
2. imports
3. public types
4. internal/private helpers close to what uses them

Within a class:

1. public API
2. internal coordination logic
3. private helpers

Match the repository if it already uses a different but consistent order.
