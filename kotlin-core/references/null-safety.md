# Null Safety

Use this reference when designing or reviewing Kotlin types and nullable control flow.

## Nullability defaults

- Default to non-null types.
- Make a type nullable only when `null` is a real domain value or an unavoidable boundary condition.
- If `null` means multiple things, replace it with an explicit model.

## Preferred patterns

Prefer:

- safe calls: `?.`
- Elvis for defaults or early exits: `?:`
- early return for invalid or absent inputs
- safe casts: `as?`
- narrowing nullable values as close as possible to their source

Good patterns:

```kotlin
val user = repository.find(id) ?: return null
val name = input?.trim().takeUnless { it.isNullOrEmpty() } ?: return ValidationError
```

## `!!` policy

Treat `!!` as a last resort.

Allowed only when:

- the invariant is immediate and obvious
- a framework callback guarantees non-null but Kotlin cannot express it cleanly
- replacing it would make the code significantly less clear and the risk is controlled

If `!!` crosses a boundary, remove it.

## Platform types and Java interop

Normalize Java platform types quickly:

- convert incoming platform values to explicit nullable or non-null Kotlin types
- do not let platform uncertainty spread through the codebase

Prefer wrappers like:

```kotlin
val value: String? = javaApi.getValue()
```

instead of carrying platform types far from the boundary.

## API design and nullability

- Returning nullable is good when “not found” or “not present” is the whole story.
- Returning sealed results is better when absence competes with multiple failure modes.
- Nullable parameters should mean something concrete, not “maybe the caller forgot”.

## Collections

- Prefer `List<T>` over `List<T?>` unless null elements are meaningful.
- Use `filterNotNull()` when cleaning boundary inputs.
- Avoid nested nullability unless it is truly necessary.

## Construction

- Prefer constructor invariants over partially initialized objects.
- Avoid `lateinit` unless lifecycle or framework integration truly requires it.
- Be careful with open members during construction.

## Review questions

- Should this type be nullable at all?
- Is `null` standing in for a richer state model?
- Can this be normalized earlier?
- Is `!!` hiding a missing invariant?
