# Android Platform

Этот файл нужен для пробелов, которые лежат между “чистая архитектура приложения” и “реальная Android-платформа”.

## Что пока не покрыто

- runtime permissions
- deep links and app links
- notifications
- sharing and external intents
- file pickers, camera, media
- lifecycle edges around platform callbacks

## Что будущий skill должен уметь решать

- когда permission запрашивать, а когда сначала объяснять
- как не размазывать platform callbacks по всему коду
- где держать intent parsing
- как не смешивать navigation state и deep link state
- как моделировать notification entry points

## Какие decision rules нужны

- когда permission logic живет в UI, а когда в coordinator/viewmodel-adjacent layer
- когда deep link должен вести прямо в screen route, а когда через intermediate resolver
- когда external result нужно сразу превращать в domain action
- как отделять platform events от persistent `UiState`

## Какие anti-patterns надо запретить

- permissions scattered across random composables
- deep link parsing directly in UI nodes
- notification payload logic inside unrelated screens
- intent extras leaking through multiple layers without normalization

## Минимальный reference pack на будущее

- permission flow patterns
- deep link routing examples
- notification tap handling
- activity result integration
