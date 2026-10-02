## 1. Контракты и входная валидация

- [x] 1.1 Обновить полный OpenAPI по новой выгрузке, Skills/Domains с замыканием ссылок и документацию происхождения/ограничений; выполнить `yarn api:generate`. Проверка: 40 операций/156 схем, новый minimum weight и UUID группы, сохранены все прежние API/security metadata; standalone contract tests и `yarn api:check` проходят без Downloads.
- [x] 1.2 Согласовать общую request-schema фраз и всех её потребителей (мастер, редактор, API client) с weight >= 0 и UUID группы без ужесточения response. Проверка: unit/client-тесты принимают 0, default 1 и UUIDv4, отклоняют отрицательный weight/malformed UUID без потери данных, сохраняют остальные ограничения.

## 2. Моки

- [x] 2.1 Обновить существующие mocks под request-ограничения и дополнить HTTP-тесты PUT intents. Проверка: 0/omitted/negative weight, UUIDv4/malformed ID, GET сохранённого набора, неизменность данных при 422, replay/clear; `node --test mocks/*.test.mjs`.
- [x] 2.2 Дополнить существующее покрытие POST status тремя UI-переходами и coherent detail/list. Проверка: target status, однократная версия, сохранение intents, replay, stale-version, key/body conflict, невалидный enum и неизменность при отказе; README отличает mock-конвенции от production, не добавлены новые маршруты/таймеры/auth.

## 3. Клиент и шкала MOS-909

- [x] 3.1 Добавить entities/skill status client/mutation с существующей detail schema, expected_version, Idempotency-Key и обновлением Query cache без retry. Проверка: client/hook-тесты точных method/path/body/headers, валидного/невалидного ответа и invalidation detail/list без устаревшего overwrite.
- [x] 3.2 Создать feature skill-lifecycle и скомпоновать шкалу в карточке над вкладками, используя текущий detail и ручное обновление. Проверка: component-тест всех восьми текущих статусов, neutral остальных этапов, aria-current, отсутствия вымышленных результатов/ETA и мутаций при открытии; read-only badge и соседние вкладки сохранены.

## 4. Одиночные команды

- [x] 4.1 Реализовать матрицу draft→checking, sandbox→review, whitelist→prod и доступное подтверждение с именем/ID/целью и snapshot версии. Проверка: component-тест команд для каждого статуса, отмены без POST, изменения snapshot, double-click и явного подтверждения prod; нет ручного завершения проверок/ревью и обхода матрицы.
- [x] 4.2 Обработать подтверждённый успех, несовпадающий target, 422/409, stale read и неизвестный исход без автоматического POST. Проверка: component-тест network/timeout/5xx/невалидного DTO, блокировки до успешного GET, ошибки refetch, нового осознанного подтверждения после чтения, отсутствия повторного запроса со свежей версией без пользователя и согласованного реестра.

## 5. Приёмка

- [x] 5.1 Обновить только устаревшие lifecycle-запреты в существующих component-тестах и проверить регрессии анкеты/фраз/подключения/мастера. Проверка: GET-only открытие, строгий неизвестный status, отсутствие auth/review/bulk/global-toggle операций; FSD public imports и владельцы declarations соблюдены.
- [x] 5.2 Выполнить `yarn typecheck`, `yarn lint` без предупреждений, `yarn test`, `yarn format:check`, `yarn api:check`, strict OpenSpec validation и diff review; `yarn build` при изменении сборки. Зафиксировать PASS/FAIL/not run с причинами; browser/E2E не создавать, не менять, не запускать. Проверить согласованность delta с соседними lifecycle changes и отдельно перечислить принятые допущения/отсутствующие backend-гарантии в итоговом отчёте.
