# Modularization And Build

Этот файл нужен для роста проекта beyond one-app-module architecture.

## Что пока не покрыто

- module boundaries
- shared core modules
- feature modules
- build logic extraction
- Gradle convention plugins
- product flavors and environment separation

## Что будущий skill должен уметь решать

- когда модульность оправдана, а когда это premature complexity
- как разрезать app by feature vs by responsibility
- где держать shared UI, shared domain, shared data contracts
- как не превратить modularization в build-time pain without payoff

## Какие decision rules нужны

- modularization should serve ownership, build performance, or isolation
- do not split modules before boundaries are real
- shared modules need clear ownership rules
- flavors should reflect deployment reality, not random config sprawl

## Какие anti-patterns надо запретить

- module explosion
- common/core modules with no clear purpose
- duplicated build config across modules
- environment logic scattered in code instead of build config boundaries

## Минимальный reference pack на будущее

- module boundary heuristics
- convention plugin structure
- flavor and build type strategy
