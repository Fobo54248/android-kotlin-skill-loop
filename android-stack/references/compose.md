# Compose

Use this reference for Compose UI structure and rendering boundaries.

## Compose posture

Compose should be declarative, state-driven, and easy to reason about.

## Good Compose structure

- screen-level composable receives state and callbacks
- reusable child composables are mostly stateless
- preview-friendly components are isolated from app wiring
- side effects are localized and intentional

## State ownership

Hoist state unless it is:

- ephemeral visual UI state
- local interaction state with no architectural value outside the composable

Examples of local state:

- dropdown expanded flag
- temporary text field editing state before submit
- pager or tab selection when not needed elsewhere

## Avoid

- repository calls from composables
- direct ViewModel creation inside deeply nested UI nodes
- hard-coded navigation behavior inside reusable components
- large composables doing layout, business branching, and side effects all at once

## Reuse

Extract components when:

- repeated UI appears
- readability improves
- previews become easier

Do not extract tiny wrappers with no semantic value just to increase file count.
