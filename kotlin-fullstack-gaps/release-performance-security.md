# release performance security

Этот файл нужен для production-hardening, а не для повседневной feature coding.

## Что пока не покрыто

- release build behavior
- R8 / shrinking / obfuscation strategy
- startup and runtime performance
- secrets handling
- encrypted local data
- network security basics
- crash, logging, and observability decisions

## Что будущий skill должен уметь решать

- как проверять production-readiness before ship
- какие performance issues ловить на уровне архитектуры
- как не хранить чувствительные данные как попало
- где заканчивается app architecture и начинается security discipline

## Какие decision rules нужны

- production logging should be intentional
- secrets do not belong in source or plain preferences
- release verification must differ from debug confidence
- performance work should target known pressure points, not vague micro-optimizations

## Какие anti-patterns надо запретить

- assuming debug behavior equals release behavior
- storing tokens or secrets casually
- shipping without thinking about shrinker rules
- performance “fixes” with no measurement

## Минимальный reference pack на будущее

- release checklist
- security baseline
- startup performance checklist
- persistence and secret storage rules
