# Data Layer

Use this reference for DTOs, Room entities, repositories, and mapping rules.

## DTO rules

- DTOs mirror remote payloads
- serialization annotations stay here
- normalize API awkwardness here or at the repository boundary
- avoid leaking transport naming or nullability into UI

## Entity rules

- entities mirror storage needs
- Room annotations stay here
- entities can differ from DTOs and domain models
- schema changes should be intentional

## Domain mapping

Map into domain when:

- business meaning matters
- multiple data sources feed the same feature
- the UI should not know transport or storage details

## Repository rules

Repository should answer:

- where data comes from
- when to use local vs remote
- how to merge or refresh sources
- what model upper layers should consume

Repository should not become:

- a god object for the whole app
- a bag of pass-through functions without ownership

## Caching

Be explicit about cache policy:

- remote-first
- local-first
- write-through
- refresh-on-open

Do not leave freshness behavior implicit if user-visible behavior depends on it.
