# Paging

Этот файл нужен для long lists, pagination, remote mediation и incremental loading UX.

## Что пока не покрыто

- Paging 3
- paging source vs remote mediator
- append/prepend/loading states
- cached paging data
- Compose integration around paged lists

## Что будущий skill должен уметь решать

- когда действительно нужен Paging, а когда достаточно page-based manual loading
- где держать paging policy
- как моделировать first load vs append load vs refresh
- как соединять paging with Room and network

## Какие decision rules нужны

- не использовать Paging ради маленьких списков
- if list can grow large and refresh incrementally, Paging is justified
- append errors should not look like first-load errors
- refresh behavior should preserve as much user context as possible

## Какие anti-patterns надо запретить

- hiding pagination complexity inside UI-only hacks
- one loading flag for initial load and append load
- mixing paged transport models directly in UI

## Минимальный reference pack на будущее

- paged repository structure
- LoadState UI patterns
- Room + Paging integration
