# Tasks

## 1. Contract boundary and surface API

- [x] 1.1 Перед реализацией подтвердить в change review матрицу переходов и источник embed-кода; если backend не уточняет их, принять зафиксированный fallback «серверный ответ авторитетен, действия не фильтруются guessed state machine, embed-код только из detail» и проверить, что proposal/design/spec не обещают генерацию или fictitious token.
- [x] 1.2 Расширить `entities/surface` типами и runtime-схемами для `SurfaceStatusResponse`, lifecycle actions и `UpdateSurfaceConfigurationRequest/Response`, используя generated `components` без ручного дублирования DTO; проверить API-client unit-тестами валидный ответ, невалидный status/date и HTTP error.
- [x] 1.3 Добавить в surface API client вызовы шести POST-операций и `PUT /configuration`, а в model — mutation/query-refresh controller с единственным pending guard, сохранением последнего action для retry и обновлением detail/list cache; проверить endpoint mapping, отсутствие тела у lifecycle POST и повтор запроса после ошибки.

## 2. Lifecycle UI and publication flow

- [x] 2.1 Добавить в `widgets/surface-details` блок «Жизненный цикл конфигурации» с серверным статусом и шестью действиями, соблюдая FSD-размещение props/types/handlers и блокируя только конкурирующие операции на время запроса; component-тестом проверить labels, request mapping, status response и отсутствие локальной state machine.
- [x] 2.2 Добавить controlled publish confirmation dialog на существующих `Dialog` primitives: отмена не отправляет POST, подтверждение отправляет только `/publish`, success-состояние открывается лишь после успешного ответа, а фокус/закрытие доступны с клавиатуры; покрыть component-тестами cancel, success и rejected publish.
- [x] 2.3 Добавить widget-owned accessible feedback для copy/lifecycle/configuration с `role=status`/`role=alert`, сообщениями об успехе и ошибке, сохранением старого snapshot и retry последнего действия; component-тестом проверить отсутствие ложного успеха, retry и защиту от двойного клика.
- [x] 2.4 После успешного lifecycle/configuration mutation подключить полный detail refetch и обработать сбой refresh отдельным предупреждением с retry, не очищая карточку и черновик сценариев; component-тестом проверить обновление `status`, `updated_at`, configuration/connection и сохранение данных при ошибке чтения.

## 3. Server-owned placement code and configuration seam

- [x] 3.1 Сохранить вывод `connection.embed_code` как текст и подключить copy feedback к существующей Clipboard API helper: передавать исходную multiline-строку без trim/добавления атрибутов, отключать кнопку для `null`/blank и не добавлять fake token; component/unit-тестами покрыть exact copy, resolve-after-click, reject/unavailable API и отсутствие `script`-исполнения.
- [x] 3.2 Подключить typed `PUT /configuration` только для фактического сохранения конфигурации и не вызывать его как скрытый шаг publish/lifecycle; API/component-тестом проверить контрактный payload, refresh detail после успешного save и отсутствие blind PUT из publish flow при сохранении текущего placeholder-конфигуратора.
- [x] 3.3 Расширить `mocks/surfaces.mjs`/server tests для шести lifecycle endpoints: проверить `SurfaceStatusResponse`, обновление team relation, последующий GET, unknown surface и повтор после ошибки; документировать fallback previous-status mock-конвенции как dev-only и не добавлять в seed фиктивный credential.

## 4. Project verification and handoff

- [x] 4.1 Запустить `yarn test` и убедиться, что component/unit и Node mock tests проходят, включая новые сценарии lifecycle, publication, copy и retry; E2E/browser-тесты не создавать и не запускать.
- [x] 4.2 Запустить `yarn typecheck`, `yarn lint` с нулём предупреждений и `yarn format:check`; если OpenAPI/generated types изменялись — дополнительно запустить `yarn api:check` и устранить только относящиеся к change ошибки.
- [x] 4.3 Просмотреть diff change и исходников перед завершением: убедиться, что нет auth/session/RBAC, фиктивных токенов, статических success-проверок, случайных файлов, новых зависимостей без обоснования или изменений E2E; зафиксировать в итоговом отчёте пройденные, упавшие и не запускавшиеся проверки.
