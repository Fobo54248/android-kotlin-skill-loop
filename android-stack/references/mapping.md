# Mapping

Use this reference for deciding where mappings live and how explicit they should be.

## Core rule

Mapping belongs near the boundary that needs translation.

Common examples:

- DTO to domain at repository boundary
- DTO to entity when caching raw or normalized remote data
- entity to domain when storage differs from product meaning
- domain to UI-facing item model when the screen needs presentation shaping

## Good mapping traits

- explicit source and target types
- local ownership is obvious
- naming is boring and predictable
- logic is short enough to review quickly

Examples of clear names:

- `fun UserDto.toEntity(): UserEntity`
- `fun UserEntity.toDomain(): User`
- `fun Article.toListItem(): ArticleListItemUiModel`

## Where to place mappers

Good options:

- next to the source and target models when the feature is small
- inside the feature's data package when mapping is feature-specific
- in a dedicated mapper file when the conversion is meaningful and reused

Avoid:

- one global `Mappers.kt` for the whole app
- extension dumps with unrelated conversions
- hiding important business normalization deep in utility packages

## Decision rules

Use extension functions when:

- the conversion is straightforward
- discoverability helps
- the ownership is clear

Use named mapper objects or classes when:

- the conversion has dependencies
- the mapping is configurable
- the logic is large enough to deserve explicit ownership

## Anti-patterns

- DTOs leaking upward because mapping “feels repetitive”
- mapping directly to UI in the data layer without intent
- mixing field cleanup, error translation, and business policy in one opaque function
