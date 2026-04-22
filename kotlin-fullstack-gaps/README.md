# kotlin fullstack gaps

Это рабочая заготовка под пробелы, которые пока не покрыты `kotlin-core` и `android-stack`.

Смысл папки:

- не раздувать текущие skills раньше времени
- зафиксировать, чего не хватает до более полного Kotlin fullstack skill
- держать каждую большую тему в отдельном файле

Текущие крупные пробелы:

- Android background work и long-running jobs
- DataStore и app-level local preferences/state
- Paging и большие списки
- permissions, deep links, notifications, external intents
- offline-first, sync и cache policies
- modularization, build logic, flavors, dependency boundaries
- performance, security, release concerns
- backend Kotlin
- Kotlin Multiplatform
- integration and end-to-end testing strategy

Порядок добивки я бы держал такой:

1. `android-platform.md`
2. `workmanager.md`
3. `datastore.md`
4. `paging.md`
5. `offline-sync.md`
6. `modularization-build.md`
7. `release-performance-security.md`
8. `ktor-backend.md`
9. `kmp.md`
10. `testing-integration.md`
