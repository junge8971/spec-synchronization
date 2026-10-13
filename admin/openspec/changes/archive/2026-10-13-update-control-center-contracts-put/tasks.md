## 1. Контракты и документация

- [x] 1.1 Обновить общий OpenAPI из зафиксированного newcontract.json, сохранив экспортное дополнение и AND security. Проверить 111 операций, 351 схему, точные method/path и отсутствие неразрешённых refs тестами contract-documents.
- [x] 1.2 Пересобрать секционные JSON и добавить managed-resources.openapi.json с 43 операциями и замкнутым набором schemas. Проверить точное совпадение секций с общим контрактом без изменения отдельного MPMM-контракта.
- [x] 1.3 Сохранить CRUD-описание в docs/api/contracts/crud-api.md, добавить managed-resources.md, актуализировать README, затронутые обзоры и AUDIT. Проверить ссылки, происхождение/hashes, частичную семантику PUT и явное отличие опубликованных API от реализованного UI.
- [x] 1.4 Запустить yarn api:generate, адаптировать SavedDialogFilter к квалифицированной dialog-схеме. Проверить yarn api:check и существующие тесты чтения/создания/применения фильтров; не редактировать generated DTO вручную.

## 2. PUT для текущих редакторов

- [x] 2.1 Перевести сохранение навыка, connection и домена на PUT в предметных клиентах. Обновить клиентские тесты: точный метод/body/ключ, POST создания без изменений, ручной retry без PATCH fallback.
- [x] 2.2 Обновить component/session test doubles, завязанные на PATCH. Проверить успешное сохранение, конфликт версии с сохранением dirty-ввода, отсутствие запроса при невалидном вводе и отмене; не ослаблять существующие session assertions.

## 3. Совместимость mock server

- [x] 3.1 Добавить четыре PUT operationId к существующим handlers domains/skills/teams/member и idempotency для PUT навыков/доменов. HTTP-тестами проверить PUT→GET, сохранение PATCH, replay без новой мутации, 409 при изменённом теле с прежним ключом и устаревшей версии, 422 невалидного ввода.
- [x] 3.2 Добавить явный перечень 43 managed-resource unavailable-операций с 501 после валидации. Проверить startup/Ajv, недоступный read и write без изменения state, невалидный input, точное покрытие перечня и ошибку при потере handler вне перечня. Общий fallback и пропуск префикса запрещены.
- [x] 3.3 Согласовать contract tests и docs моков с новым множеством операций. Проверить сохранность intents/status/экспорта, demo-каталога и 403/500/delay, особого режима /me; fingerprint обновить с проверкой бизнес-содержимого DTO, не удалять проверки.

## 4. Согласование feedback plans

- [x] 4.1 Обновить источники и HTTP PATCH→PUT в mos-1249-feedback-api, mos-1251-feedback-editor, mos-1254-feedback-questions, mos-1256-feedback-lifecycle, mos-1259-feedback-saved-filters. Сохранить имена *Patch/EMPTY_PATCH, scope и task checkboxes; обозначить замену unavailable handlers в будущей feedback реализации. Проверить diff всех затронутых artifacts и openspec validate для каждого изменённого change.

## 5. Итоговая проверка

- [x] 5.1 Выполнить yarn api:check, yarn typecheck, yarn lint, yarn test, yarn format:check и yarn build. Проверить production isolation моков штатными проверками; E2E/browser не запускать. Отдельно перечислить пройденные, упавшие и не запущенные команды с причинами.
- [x] 5.2 Просмотреть итоговый diff: только согласованный scope, без изменений auth, новых CRUD-экранов, ослабления правил или удаления входного newcontract.json. Зафиксировать, что реальная PUT/WAF-интеграция требует отдельного подтверждения перед выпуском и не доказана локальными тестами.

## Результаты реализации — 13.10.2026

- `yarn api:check`, `yarn typecheck`, `yarn lint` (без предупреждений), `yarn format:check`, `yarn build` — пройдены. После последних тестовых правок повторены typecheck, целевой ESLint и format:check.
- Финальный `yarn test`: 113 файлов / 1092 unit/component-теста и 84 server/config-теста, все пройдены. Первоначальный сбой старого business fingerprint исправлен после независимой сверки новой выгрузки с экспортным дополнением.
- HTTP-тесты и Vite build первоначально блокировались sandbox с listen EPERM; повторены с разрешённым loopback listener и пройдены. Production isolation проверена config-тестами; mock-маркеры в build/client не найдены.
- OpenSpec strict validation текущего change и пяти затронутых feedback changes пройдена. Контракты сверены с newcontract.json: только согласованная security-нормализация и сохранённый экспорт. Исходный hash newcontract.json не изменён.
- Diff просмотрен: runtime auth, зависимости, настройки сборки и E2E не менялись. E2E/browser и реальная PUT/WAF-интеграция не запускались; gate стенда остаётся открытым перед выпуском. Коммиты не создавались.
