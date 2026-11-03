## ADDED Requirements

### Requirement: Response templates optional ownership exception

В дополнение к существующим адресным optional-исключениям правила SHALL разрешать предметный код шаблонов ответов в `app/optional/response-templates/` ради независимого удаления. Это адресное расширение правила Application code respects FSD ownership and public APIs SHALL NOT давать исключений другим модулям или ослаблять существующие границы. Композиция приложения SHALL обращаться через публичный index.ts; framework-конфигурация SHALL сохранять штатные route entrypoints. Модуль SHALL зависеть только от собственного кода, shared и публичных API entities. Другие бизнес-слайсы, shared и optional-модули MUST NOT импортировать response-templates; response-templates MUST NOT импортировать другие optional-модули, чужие pages/widgets/features или application internals. Проверки SHALL охватывать relative/type-only импорты и re-export, размещение деклараций и один компонент на файл без новых широких исключений. Правила проекта и lint SHALL описывать одинаковую адресную границу.

#### Scenario: Permitted dependencies

- **WHEN** response-templates импортирует shared либо публичный API entities, а композиция подключает его index.ts
- **THEN** архитектурная проверка разрешает зависимость и сохраняет остальные структурные проверки

#### Scenario: Cross module import

- **WHEN** response-templates импортирует код базы знаний либо другой optional-модуль импортирует response-templates, включая относительный type-only импорт или re-export
- **THEN** проверка отклоняет импорт, даже если он проходит через публичный index.ts

#### Scenario: Internal API bypass

- **WHEN** внешний потребитель обращается к внутреннему файлу response-templates вне штатного framework route entrypoint
- **THEN** проверка отклоняет зависимость, включая алиас и относительный путь
