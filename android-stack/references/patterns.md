# Patterns

Use this reference for choosing a screen-state and feature structure pattern.

## Common screen patterns

### Static or simple detail screen

Good fit:

- one `data class UiState`
- one initial load
- optional retry handling

### Cached content plus refresh

Good fit:

- content remains visible
- refreshing is modeled separately from first-load
- repository may expose observed local data plus remote refresh action

### Search or filtering screen

Good fit:

- query state in ViewModel
- derived or combined state streams
- debounce and cancellation handled clearly

### Paginated list

Good fit:

- append state separated from initial loading state
- error handling distinguishes first-load vs append failure
- list content can remain visible while more items load

### Form screen

Good fit:

- editable field state
- validation state
- submit progress
- submit success or failure events modeled clearly

## Feature packaging patterns

### Feature package

Good when a feature owns:

- screen
- ViewModel
- use case
- repository interface or implementation
- models specific to that feature

### Shared layer plus feature UI

Good when:

- the app is still small
- features share most data logic
- introducing many vertical packages would add noise

## Decision rules

- if a screen can show previous content while refreshing, do not collapse refresh into the same UX as first-load
- if errors and content can coexist, model that clearly
- if screen modes are mutually exclusive, sealed state is often clearer
- if many screens share the same state pattern, reuse the approach, not necessarily the exact base class
