# WorkManager

Этот файл закрывает background work, deferred jobs и надежное выполнение задач вне активного экрана.

## Что пока не покрыто

- one-time background work
- periodic work
- retry policies
- constraints
- foreground vs background execution boundaries
- orchestration with sync or upload flows

## Что будущий skill должен уметь решать

- когда нужен WorkManager, а когда достаточно coroutine from app scope
- когда задача должна быть guaranteed, а когда best-effort
- как проектировать worker input/output
- как не дублировать business logic между worker и repository

## Какие decision rules нужны

- WorkManager для durable background jobs, а не для любой асинхронщины
- repository/use case должны содержать business action, worker должен быть orchestration shell
- retry strategy должна быть осознанной, а не “поставим retry и посмотрим”
- constraints должны отражать реальную потребность сети, charging, idle state

## Какие anti-patterns надо запретить

- heavy business logic directly inside worker
- worker talking to UI state
- duplicated sync logic in ViewModel and Worker
- periodic work without clear product need

## Минимальный reference pack на будущее

- worker design patterns
- idempotency
- retries and backoff
- sync scheduling patterns
