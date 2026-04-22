# ViewModel And State

Use this reference for `UiState`, events, intent handling, and Flow in presentation.

## Basic pattern

- UI emits user actions
- ViewModel interprets them
- ViewModel invokes repository or use case work
- ViewModel updates immutable state
- UI renders state

## `UiState`

Choose the shape that matches the screen:

- `data class` when the screen has steady fields that change over time
- sealed state when screen modes are genuinely distinct

## Events

Keep one-time events separate from persistent state.

Examples:

- navigation request
- snackbar
- toast
- permission prompt request

Avoid replay bugs caused by storing transient events inside long-lived state objects without a consumption model.

## Loading

Be explicit about loading behavior:

- first load
- pull to refresh
- pagination append
- retry after error

These are often different UI states and should not be collapsed carelessly.

## Flow in ViewModel

- expose immutable `StateFlow`
- convert repository streams into UI-facing state
- avoid over-collecting multiple sources with unclear ownership
- keep collection logic readable

## Review questions

- Is the ViewModel the owner of screen state?
- Are one-time events separated correctly?
- Is the state easy to test?
- Can the UI be previewed or rendered from the state alone?
