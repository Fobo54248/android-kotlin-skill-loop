---
name: android-stack
description: Use when working on Android apps built with Kotlin, Jetpack Compose, MVVM, Navigation, Hilt, Retrofit, Room, and Kotlin Flow. Apply this skill when implementing features, reviewing architecture, debugging state flow, refactoring layers, wiring dependency injection, handling local and remote data, or structuring Android code across DTO, Entity, Domain, Repository, UseCase, ViewModel, and UiState.
---

# Android Stack

Use this skill for feature work in Android apps that follow a layered Kotlin architecture with Compose UI, ViewModel-driven state, dependency injection, network access, local persistence, and reactive data flow.

This skill is the Android-specific companion to a general Kotlin skill. Use it when the work is not just “write Kotlin”, but “write Android feature code with a clear app architecture”.

## Scope

This skill is designed for Android projects using:

- Kotlin
- Jetpack Compose
- MVVM
- Navigation
- Hilt
- Retrofit
- Room
- Kotlin Flow
- layered models such as DTO, Entity, Domain, Repository, UseCase, ViewModel, and UiState

It is suitable for:

- new feature implementation
- screen wiring
- data flow design
- architecture refactors
- code review
- bug fixing in state, mapping, or repository logic
- migration toward a cleaner layered structure

## Architectural intent

Optimize for:

- clear boundaries between layers
- predictable state from data source to UI
- unidirectional data flow
- framework concerns staying in framework layers
- business logic remaining testable
- incremental cleanup over rewrite-heavy “architecture purity”

## Core workflow

### Step 0: Detect the project shape

Inspect the codebase before changing anything:

- module structure
- package structure
- whether the project is feature-based, layer-based, or hybrid
- Compose vs XML usage
- navigation approach
- DI setup
- network stack
- persistence stack
- test setup
- result/error conventions

Read first:

- `build.gradle.kts` or module Gradle files
- `settings.gradle.kts`
- app module structure
- one representative feature from UI to data

Do not assume the project is already cleanly layered, even if the libraries are present.

### Step 1: Identify the task mode

Classify the task before implementing:

- new feature
- screen integration
- bug fix
- refactor
- migration
- review
- architecture cleanup

Then identify which layers are affected:

- UI only
- ViewModel and state
- domain and use cases
- repository coordination
- remote data
- local database
- navigation wiring
- dependency injection

### Step 2: Choose the smallest valid slice

Prefer small, complete vertical slices over giant partial rewrites.

A healthy implementation slice usually looks like:

1. define or adjust domain model
2. define UI state and actions
3. add use case if the business action needs one
4. extend repository boundary
5. add or update data source models and mappers
6. wire ViewModel
7. connect Compose UI
8. add DI and navigation glue
9. verify with tests where appropriate

### Step 3: Keep ownership clear by layer

Use the following layer responsibilities unless the repository has an established alternative:

- transport layer handles API request and response shapes
- persistence layer handles Room entities and DAO access
- domain layer models business meaning
- repository layer coordinates data sources and mapping
- use case layer exposes focused business operations
- presentation layer owns screen state and user intent handling
- Compose layer renders state and emits events upward

### Step 4: Verify state flow and layer boundaries

Before considering the work complete, check:

- UI does not talk directly to Retrofit or Room
- ViewModel does not own navigation controller or Android widgets
- repositories do not leak DTOs into UI
- Room entities are not casually used as screen models
- mutable state is not exposed publicly
- Flow and suspend are used intentionally
- errors are handled consistently across the feature

### Step 5: Choose pragmatic architecture, not ceremony

If two approaches are both valid, prefer the one that:

- keeps boundaries understandable
- reduces future confusion
- matches the repository's current style
- avoids introducing unused abstraction
- keeps tests straightforward

Do not add extra layers just to satisfy a diagram.

## Recommended project flow

Preferred direction of dependencies:

`API / DB -> data source -> repository -> use case -> ViewModel -> UiState -> Compose UI`

Common runtime flow:

1. API returns network payload
2. DTO is parsed
3. DTO maps to domain or persistence shape
4. database stores or emits entity updates
5. repository combines sources
6. use case shapes business-facing output
7. ViewModel exposes `StateFlow<UiState>`
8. Compose screen renders immutable state

## Decision rules

Use this section to make design choices consistently.

### When to use `suspend` vs `Flow`

Use `suspend` when:

- the caller asks once and expects one answer
- the work is a command such as save, delete, refresh, submit, login
- observation over time is not part of the feature

Use `Flow` when:

- the UI should react to changing local data
- multiple sources combine into one evolving state
- refreshes, filters, search, or paging update over time
- the screen benefits from continuous observation

Avoid `Flow` when it only wraps one immediate value and adds collector complexity without benefit.

### When a `UseCase` is worth having

Add a use case when:

- a business action has a meaningful name
- multiple repositories or policies are coordinated
- the ViewModel would otherwise become policy-heavy
- the same action may be reused by more than one screen

Skip a dedicated use case when:

- the repository call is already the business action
- wrapping it would create pure ceremony
- the feature is small and the extra layer adds no clarity

### When to use `data class UiState` vs sealed state

Prefer `data class UiState` when:

- the screen is always present
- most fields coexist at the same time
- loading and error can be represented as flags or subfields without confusion

Prefer sealed state when:

- the screen has truly different modes
- content and error states are structurally different
- the screen should never render certain fields together
- representing everything in one data class would produce ambiguous combinations

### When to map `DTO -> Domain` directly

Map `DTO -> Domain` directly when:

- there is no local persistence layer involved
- the payload shape is already close to domain meaning
- the feature is simple and storage is not part of the flow

Map `DTO -> Entity -> Domain` or use both persistence and domain mappings when:

- local cache matters
- storage shape differs from domain meaning
- offline or refresh behavior matters
- multiple screens depend on persisted data

### When to split by feature vs by layer

Prefer feature-oriented grouping when:

- the app has multiple product areas
- each feature owns UI, ViewModel, repository wiring, and local models
- team navigation through the codebase benefits from vertical ownership

Prefer layer-oriented grouping when:

- the app is small
- features are not numerous yet
- a simple separation is easier to maintain

Do not reorganize the repository purely for architectural aesthetics unless the current shape is actively slowing work down.

## Layer rules

### DTO

Use DTOs for transport shapes only.

- keep serialization annotations here
- match external API structure here
- normalize awkward payloads as early as possible
- do not pass DTOs into ViewModel or Compose

Read `references/data-layer.md` for mapping and remote guidance.

### Entity

Use entities for Room persistence models.

- keep Room annotations here
- represent storage shape, not screen shape
- avoid using entities as a shortcut UI model
- keep schema changes deliberate and migration-aware

### Domain

Use domain models for business meaning.

- keep them framework-light
- name them around the app’s real concepts
- prefer them in use cases and presentation boundaries
- avoid transport or persistence annotations here

### Repository

Repository owns orchestration.

- choose between local and remote sources
- combine sources when needed
- map between DTO, Entity, and Domain
- expose `suspend` for one-shot operations
- expose `Flow` for observed or streaming data

Do not turn repositories into giant dumping grounds for unrelated features.

Repository ergonomics:

- repository methods should read like product behavior, not transport detail
- hide whether data came from API or database unless the caller truly needs to know
- avoid naming methods after HTTP verbs when domain language is clearer
- keep refresh, cache, and merge behavior explicit

### UseCase

Use cases should be focused and intentional.

- one business action or one meaningful query per use case
- keep them thin when business logic is small
- keep them richer when orchestration or policy belongs above repository level
- `operator fun invoke(...)` is fine if the codebase already uses it consistently

Do not add ceremonial use cases that simply forward one method with no architectural benefit.

Good use case names usually read like product intent:

- `GetFeed`
- `ObserveProfile`
- `RefreshMessages`
- `UpdateSettings`

Less helpful names:

- `FeedRepositoryUseCase`
- `UserInteractorHelper`
- `DataProcessor`

### ViewModel

ViewModel owns presentation state.

- collect flows in `viewModelScope`
- expose immutable state
- transform repository or use case outputs into screen-friendly models
- handle user intents and screen events
- keep Android UI primitives out of business logic

Do not:

- inject navigation controllers
- call Retrofit directly
- embed SQL or DAO logic
- expose mutable flow/state objects publicly

ViewModel ergonomics:

- UI-facing state names should be obvious to screen readers of the codebase
- state updates should be traceable without jumping through many helper layers
- user intent handlers should read in event language such as `onRetry()`, `onSearchQueryChanged()`, `onSaveClicked()`

### UiState

UI state must be explicit and stable.

Use:

- `data class` for stable screens where fields update over time
- sealed interface or sealed class for distinct screen modes such as loading, content, empty, and error

A good `UiState`:

- is immutable
- is easy to preview
- is easy to test
- tells the UI everything it needs without extra hidden work

A bad `UiState` often:

- mixes durable state with one-time events
- uses nullable fields for mutually exclusive modes without explanation
- requires the composable to infer business logic that belongs in ViewModel

## Compose guidance

Compose should be the rendering layer, not the business layer.

### Compose rules

- pass state down, events up
- hoist state unless it is truly local UI-only state
- keep composables focused and previewable
- extract reusable UI pieces when reuse or readability justifies it
- keep navigation and side effects near the screen boundary
- name composables by UI role, not implementation detail
- keep screen composables thin enough that another developer can scan them quickly

### Avoid in composables

- business logic
- repository calls
- database access
- direct mapping from DTOs
- broad coroutine launches for non-UI work

Read `references/compose.md` for more detailed UI guidance.

## ViewModel and Flow guidance

The default presentation model should be:

- user actions enter ViewModel
- ViewModel calls use case or repository
- ViewModel updates `UiState`
- UI observes state via Compose

### Flow rules

- use `StateFlow` for long-lived screen state
- use `SharedFlow` or channel-like event patterns carefully for one-off events
- use plain `suspend` instead of Flow when there is only one response
- avoid turning every function into a stream out of habit
- prefer one obvious state stream over many partially overlapping ones when possible
- combine flows intentionally rather than scattering collectors across the ViewModel

### Events

Separate:

- persistent screen state
- one-time events such as toast, navigation, or snackbar requests

Do not overload one state object with transient events in a way that causes repeat delivery bugs.

Read `references/viewmodel-state.md` for detailed state handling patterns.

## Hilt guidance

Hilt owns dependency graph wiring, not business policy.

Use it for:

- Retrofit services
- Room database and DAOs
- repositories
- use cases where the codebase injects them directly
- dispatchers or other app-level dependencies when needed

Prefer:

- constructor injection by default
- modules only where construction cannot be expressed directly
- deliberate scoping

Avoid:

- giant modules with unrelated providers
- hiding feature behavior in DI wiring
- injecting more dependencies than a class actually needs

Ergonomic DI rule:

- if constructor injection expresses the dependency clearly, prefer it
- if a module is needed, keep the provider close to the ownership boundary it serves

Read `references/di.md` for detailed DI rules.

## Retrofit guidance

Retrofit is for remote boundaries.

- keep service interfaces cohesive
- use DTOs for request and response shapes
- centralize remote error translation strategy
- keep transport concerns out of UI-facing models

Be careful with:

- nullable API fields
- default values masking backend issues
- coupling response models directly to UI rendering

Remote ergonomics:

- translate transport weirdness once, near the boundary
- do not make every caller remember backend quirks
- if the API is unstable, isolate that instability in mapping code

## Room guidance

Room is for persistence boundaries.

- DAOs stay in the data layer
- entities stay persistence-oriented
- observed tables can expose Flow when the UI benefits from it
- schema changes require deliberate migration thinking

Avoid:

- querying the database from ViewModel
- spreading DAO usage outside the data layer
- treating Room entities as if they were domain language

Persistence ergonomics:

- DAO names should reflect table intent clearly
- query methods should signal whether they observe or fetch once
- if entity fields are database-shaped but not product-shaped, keep the translation explicit

## Navigation guidance

Navigation should be explicit but lightweight.

- keep route logic near screen boundaries
- pass lightweight identifiers instead of large model objects when possible
- avoid deeply coupling reusable UI components to navigation implementation
- keep argument parsing simple enough to debug quickly
- prefer stable route contracts over clever route construction

When the project uses typed or structured routes, match the existing approach instead of inventing a second routing style.

## Error handling guidance

Pick one coherent strategy per feature boundary.

Possible patterns:

- repository translates remote and local errors into domain-friendly outcomes
- ViewModel maps outcomes into `UiState`
- UI renders error state or triggers one-time error events

Avoid mixing:

- raw exceptions in some screens
- stringly typed errors in others
- partial `Result` usage without a consistent convention

Decision rule:

- if the user can realistically recover, model the failure in state
- if the failure is purely infrastructural, translate it once and keep the UI contract simple

## Feature implementation playbook

For a new feature, prefer this order:

1. clarify screen purpose and data requirements
2. define domain model if needed
3. define `UiState` and user actions
4. add or adjust API DTOs
5. add or adjust Room entities and DAO methods if local persistence is involved
6. write mapping functions
7. add repository methods
8. add use case if it adds business clarity
9. implement ViewModel state handling
10. build Compose screen
11. wire navigation
12. wire Hilt
13. add or update tests

## Ergonomic defaults

Use these defaults unless the codebase clearly prefers something else:

- one screen -> one `UiState`
- one ViewModel per screen or tightly related screen flow
- repository names in domain language, not implementation language
- mappers as explicit functions when conversion has meaning
- feature package or folder should be understandable from names alone
- side effects should be visible near the screen boundary
- navigation arguments should be small and stable
- public state from ViewModel should be immutable

## Naming guidance

Choose names that describe product meaning, not framework mechanism.

Prefer:

- `ArticleDetailsUiState`
- `ObserveCart`
- `ProfileRepository`
- `SettingsEntity`
- `UserDto`
- `ProfileScreen`
- `ProfileViewModel`

Avoid:

- `DataModel`
- `BaseUseCase`
- `CommonRepositoryImpl2`
- `UiModelData`
- `ResponseItemThing`

## Mapping guidance

Keep mapping boring and explicit.

Prefer:

- small named mapper functions
- clear one-directional conversions
- mapping close to the layer boundary that owns it

Avoid:

- hidden mapping inside random extension files with unclear ownership
- giant mapper files for the entire app
- mixing transport cleanup and domain policy in one unreadable function

Read `references/mapping.md` for more detailed mapping choices.

## State and loading patterns

Be explicit about which loading model the screen uses:

- first-load only
- pull-to-refresh
- cached content plus refresh
- pagination
- optimistic update

Do not force all screens into one generic state pattern if their UX needs differ.

Read `references/patterns.md` for common screen-state tradeoffs.

## Review checklist

Use this checklist during code review:

- Are DTO, Entity, Domain, and UI models clearly separated?
- Does repository own data-source orchestration?
- Is ViewModel free from network and database details?
- Is Compose rendering state instead of inventing business rules?
- Is `Flow` used only where stream semantics matter?
- Are one-time events separated from stable state?
- Is DI clean and minimal?
- Is navigation kept near screen boundaries?
- Are mappings explicit enough to maintain?
- Are tests aimed at behavior instead of wiring trivia?

## Anti-patterns to avoid

- DTOs flowing into Compose
- Room entities used everywhere because it is “faster”
- Retrofit calls from ViewModel
- one repository for the entire app
- use cases added purely for ceremony
- mutable state exposed from ViewModel
- navigation controller pushed into lower layers
- business logic embedded in composables
- collecting Flow in the wrong lifecycle boundary
- forcing a full clean architecture rewrite into an established codebase

## Reference map

Read only what you need:

- `references/structure.md` for package layout and layer ownership
- `references/data-layer.md` for DTOs, entities, repositories, and mapping
- `references/viewmodel-state.md` for `UiState`, ViewModel, events, and Flow usage
- `references/compose.md` for Compose screen structure and UI boundaries
- `references/di.md` for Hilt modules, scopes, and injection rules
- `references/mapping.md` for mapper placement and model conversion decisions
- `references/patterns.md` for screen-state and feature-shape patterns
- `references/testing.md` for testing strategy across layers

## Output expectations

- Prefer the smallest vertical change that cleanly fits the architecture.
- Match the repository’s current conventions where reasonable.
- Move the codebase toward cleaner boundaries without demanding a total rewrite.
- Explain tradeoffs briefly when multiple valid Android patterns exist.
