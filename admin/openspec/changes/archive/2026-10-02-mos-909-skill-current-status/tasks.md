## 1. Текущий статус карточки

- [x] 1.1 Добавить текстовый Badge статуса в SkillDetailsHeader через публичный skillStatusLabels; сохранить type/version и перенос группы без новых запросов/состояния. Проверка: параметризованный component-тест всех восьми подписей и обновления status при повторном получении/передаче карточки.
- [x] 1.2 Актуализировать интеграционный component-тест SkillDetails: серверный draft виден как «Статус: Черновик» на всех вкладках, прежний глобальный запрет слова «Черновик» заменён точными проверками отсутствия шкалы, ETA и фиктивных результатов. Проверка: тест сохраняет GET-only утверждение, отсутствие кнопок обучения/проверки/выката и работу существующих вкладок; неизвестный status показывает ошибку без подставленного значения.
- [x] 1.3 Дополнить существующую проверку detail-клиента для missing/null/нестроковых и неизвестного status, сохранив строгую схему без production-изменений. Проверка: целевые client/component-тесты проходят, все опубликованные enum принимаются, повреждённые значения отклоняются; read-model списка не меняется.

## 2. Приёмка ограниченного этапа MOS-909

- [x] 2.1 Выполнить yarn typecheck, yarn lint без предупреждений, yarn test и yarn format:check; при изменении API-типов — yarn api:check, сборки — yarn build. Проверка: записаны PASS/FAIL/not run и причины; просмотрен diff только шапки, тестов и planning artifacts, нет новых lifecycle-команд, зависимостей или изменений auth. Browser/E2E не создавать, не менять, не запускать; визуальную приёмку не заявлять, полную задачу MOS-909 не считать закрытой.

## Результаты приёмки

- PASS: `yarn typecheck`, `yarn lint` (0 warnings), `git diff --check`, `openspec validate mos-909-skill-current-status --strict`.
- PASS: целевой `yarn vitest run app/widgets/skill-details/ui/skill-details.test.tsx app/entities/skill/api/skill-details-client.test.ts --maxWorkers=2` — 63 теста. Первый запуск выявил преждевременное чтение DOM в новом тесте после refetch; проверка теперь ожидает отображения серверной версии штатным findByText, без увеличения timeout или ослабления утверждений.
- PASS: `VITEST_MAX_WORKERS=2 yarn test` — 492 Vitest-теста (54 файла) и 31 Node server/contract/FSD-тест. Ограничена только параллельность штатной переменной окружения; конфигурация и пороги не менялись. Проверка generated API входит в Node suite и прошла.
- FAIL вне diff: `yarn format:check` — три прежних архивных документа: `openspec/changes/archive/2026-09-23-connect-control-center-http-client/design.md`, `openspec/changes/archive/2026-09-23-improve-code-quality/specs/code-quality-gates/spec.md`, `openspec/changes/archive/2026-09-28-update-control-center-routing/specs/control-center-shell/spec.md`. Архив оставлен нетронутым.
- NOT RUN: отдельный `yarn api:check` и `yarn build` — API-типы и сборочная конфигурация не менялись; browser/E2E и визуальная приёмка не разрешены и не выполнялись.
- Diff просмотрен: production-изменение ограничено Badge и переносом группы в шапке; два существующих тестовых файла дополнены. Новых запросов, polling, lifecycle-команд, зависимостей, auth или изменения runtime-валидации нет. План ограниченного этапа выполнен; полный MOS-909 и основной spec не закрывались/не синхронизировались, change не архивирован.
