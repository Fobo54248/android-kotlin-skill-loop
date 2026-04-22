# Structure

Use this reference for package layout and ownership boundaries.

## Common layouts

Android projects usually fall into one of these shapes:

- by layer: `data`, `domain`, `presentation`
- by feature: `feature/home`, `feature/details`, each with nested data/domain/ui
- hybrid: top-level shared layers with feature subpackages

Do not force a new layout if the current one is consistent. Improve within the existing shape.

## Ownership rules

- UI renders state and forwards events
- ViewModel owns presentation coordination
- use case owns focused business actions where useful
- repository owns data source coordination
- remote data source owns network calls
- local data source or DAO owns persistence access

## Dependency direction

Upper layers should depend on stable boundaries, not implementation details.

Preferred direction:

`ui -> viewmodel -> usecase -> repository -> data sources`

Data models should not casually travel upward without mapping.

## Shared code

Promote code to shared modules only when more than one feature truly needs it.

Avoid turning “shared” into a dumping ground for unrelated helpers.
