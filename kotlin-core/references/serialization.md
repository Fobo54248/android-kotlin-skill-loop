# Serialization

Use this reference for DTO design, encoded formats, and schema boundaries.

## Boundary rule

Separate transport shape from business meaning unless there is a strong reason not to.

Common split:

- DTO or transport model for network or wire format
- domain model for business logic
- persistence model when storage shape differs

## Annotation placement

- Keep serialization annotations in transport models where possible.
- Avoid sprinkling wire-format concerns across domain types unless the app is intentionally simple and the tradeoff is accepted.

## Compatibility

When data crosses process, network, or storage boundaries:

- treat field names as contracts
- be deliberate about defaults
- think about missing fields, extra fields, and backward compatibility

## DTO design

- Prefer explicit field names and types.
- Avoid nullable-everything DTOs unless the upstream schema truly works that way.
- Normalize awkward external formats before they touch business logic.

## Mapping

- Keep mapping readable and explicit.
- Use dedicated mapper functions when conversion logic has meaning or branching.
- Avoid burying mapping rules deep inside unrelated classes.

## Review questions

- Is this model a transport model, domain model, or persistence model?
- Are wire concerns leaking upward?
- Are defaults and missing fields handled intentionally?
- Would schema changes break this silently?
