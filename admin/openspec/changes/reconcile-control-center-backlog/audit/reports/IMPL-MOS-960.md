# IMPL-MOS-960 — точное implementation/test evidence

## Результат и граница

**Контекст песочницы MOS-960 в проверенной точке входа не реализован:** `/sandbox` отображает общий `PlaceholderPage`. Существуют чтение метаданных сущностей и транспорт перехода поверхности в `sandbox`, но они не связаны этой страницей с серверной тестовой сессией или проверяемой версией.

Это новое сопоставление текущего кода и текстов тестов, **не повторный requirement-аудит**. Использованы `SCENARIO-MOS-960.md`, его review и решение D-012 как карта discovery с обязательными поправками. Прежнее покрытие не объявляется новым U→P; закрытие задачи не предлагается.

Проверены только MOS-960, связанная точка входа, существующие entity-клиенты и узкие тестовые границы. Реализация MOS-961/MOS-962, auth, токены и mock-политики не исследовались. Блокера для данного ограниченного анализа нет.

## Источник и принятая база

Относительно `openspec/changes/reconcile-control-center-backlog/audit/`:

- `sources/jira-sandbox-details/r1/content.json`, JSON pointers `/items/0/key`, `/items/0/description`, `/items/0/status`, `/items/0/updated`, `/items/0/comments`: MOS-960 требует страницу выбранного навыка/поверхности, endpoint, контур, состав сценариев, приветствие, состояние синхронизации, серверную тестовую сессию и связь с проверяемой версией. Отдельно запрещает приравнивать `status=sandbox` к запуску чата.
- `/items/0/status` — `Backlog`; `/items/0/updated` — `2026-10-15T14:46:55.374+0800`; получение item — `2026-10-16T13:18:06.051Z`. Собрано ноль комментариев.
- `reviews/R-SCENARIO-MOS-960.md`, разделы обязательных исправлений и nine-candidate verification: сохраняются точные DTO/статусные различия; `appearance` не переносится в доказательства.
- `decisions.md:599–611`, D-012: прежнее сопоставление принято только вместе с поправками review. Опубликованные checks не являются свидетельством тестовой сессии/ревизии.

Исторические wiki/API из прежнего отчёта заново не аудировались. Выводы ниже основаны на новом чтении текущих файлов.

## Expected / observed / unknown

| Join | Expected из `/items/0/description` | Observed: точный текущий locator | Unknown / предел |
|---|---|---|---|
| C01–C02: выбранный навык/поверхность | Страница стенда сохраняет предметный контекст | `app/shared/config/constants/application-routes.constants.ts:68–77`: статический `/sandbox`; `app/routes/sandbox.tsx:1–5`: только `<PlaceholderPage />`; `app/pages/placeholder/ui/placeholder-page.tsx:1–10`: статические «ЦАМ» / «Административная консоль». В этой цепочке нет чтения ID, загрузки сущности или создания тестовой сессии | Это доказательство состояния указанной точки входа, не утверждение об отсутствии реализации во всех внешних системах |
| C03–C06: endpoint, контур, состав, приветствие | Метаданные контекста стенда | `app/entities/skill/api/skill-details-client.ts`, `skillDetailsSchema` и `getSkillDetails`: присутствуют `connection`, `intents`, `display_version`, integer `version`; `app/entities/surface/api/surface-registry-client.ts:56–90`, `surfaceDetailsSchema`: saved `configuration.greeting`, sibling `enabled_skills` с `skill_id`/строковыми parameters. `/sandbox` эти клиенты не вызывает и поля не отображает | Нельзя объявлять saved данные фактическим составом/приветствием стенда. Источник доступного контура и точный смысл endpoint этим кодом не установлены. Вложенная skill connection schema здесь не анализировалась |
| C07: состояние синхронизации | Подтверждённое состояние стенда | В полностью прочитанной route→placeholder цепочке нет такого поля, состояния или запроса | Семантика и получение состояния остаются зависимостью MOS-962; её реализация не присваивается MOS-960 |
| C08–C09: серверная сессия и версия | Контекст тестовой сессии связан с проверяемой конфигурацией | В route→placeholder нет сессии/привязки. `skill-details-client.ts`, `changeSkillStatus`: `expected_version` используется в POST изменения статуса; это не создание тестовой сессии | Integer `version`, `display_version`, timestamp либо статус нельзя самостоятельно назначить проверяемой ревизией |
| Граница surface `sandbox` | Переход статуса не выдаётся за запуск стенда/чата | `surface-registry-client.ts:105–109`: валидируемый результат — `surface_id`, `status`, `updated_at`; `runSurfaceLifecycleAction`: POST без body, используя `surfaceLifecyclePaths`. `app/entities/surface/model/use-surface-lifecycle-mutation.ts:1–10` делегирует эту команду | Наличие транспорта не доказывает пользовательский сценарий, сессию, доступность deployment или фактическое поведение backend |

Положительное наличие entity metadata уточняет saved issue: обобщённое «контекст не определён» нельзя расширять до «никаких данных выбранного навыка/поверхности нет». Но готового **контекста тестовой сессии** проверенная страница из этих данных не строит.

## Новые точные тестовые доказательства

Тесты **только прочитаны, не запускались**.

1. **Ссылка, не реализация контекста.**  
   `app/widgets/navigation/ui/application-navigation.test.tsx:11–24` проверяет `href="/sandbox"`. Здесь нет выбранного ID, загрузки стенда или assertions о сессии.

2. **Surface sandbox — статусная команда и обновление cache.**  
   `app/entities/surface/model/use-surface-mutation-controller.test.tsx:52–102`:
   - fetch stub для `/sandbox` ожидает `POST` и `body === undefined`;
   - возвращает `surface_id/status/updated_at`;
   - вызов `run({ surfaceId, request: 'sandbox' })`;
   - проверяются обновлённые detail/registry и два fetch-вызова.

   Это конкретное покрытие lifecycle mutation, **не** тест запуска чата или привязки тестовой версии.

3. **Статус навыка не открывает песочницу.**  
   `app/widgets/skill-details/ui/skill-details.test.tsx:1150–1191` моделирует этапы до `sandbox`, проверяет только GET-запросы, прекращение дальнейшего polling и отсутствие кнопки «Открыть песочницу». Текст теста не подтверждает серверную готовность; его утверждения об автоматических проверках не переиспользуются как вывод о текущей публикации API.

4. **Surface UI намеренно не предоставляет workflow.**  
   `app/widgets/surface-details/ui/surface-details.test.tsx:143–153` при fixture `status: 'sandbox'` проверяет отсутствие кнопки запуска и блока проверки в подключении. Несмотря на широкое название теста, этот конкретный test case не перебирает все статусы.

5. **Пограничный случай: backend требует sandbox.**  
   `app/widgets/surface-details/ui/surface-details.test.tsx:618–636` моделирует `SANDBOX_CHECK_REQUIRED`: показывает сообщение, проверяет единственную lifecycle-команду `['publish']`, не открывает запуск sandbox.

Последние два пункта согласуются с `openspec/specs/surface-lifecycle-publication/spec.md:37–68`: читаемый статус `sandbox` сохраняется, UI и скрытый запуск запрещены текущей MVP-границей. Это не разрешение распространить исключение на весь будущий MOS-960.

## Минимальные dispositions и кандидаты для очереди parent

**keep — MOS-960 остаётся незакрытым.**  
Маршрут существует, но его текущая реализация — placeholder. Найденные тесты не доказывают контекст, серверную сессию и tested-version binding. Сохраняются девять уже принятых кандидатов, а не создаётся их новая копия.

**update — добавить implementation evidence к существующему MOS-960.**  
Предложение для `pending-publication.md`, только после review parent:

> В текущем frontend `/sandbox` ведёт на общий PlaceholderPage без выбора/загрузки навыка или поверхности и без тестовой сессии. Entity-клиенты уже читают часть saved metadata, а surface lifecycle transport реализует bodyless POST `/sandbox` с результатом статуса. Прочитанные тесты проверяют навигацию, статусную mutation/cache и отсутствие автоматического запуска, но не выполнение MOS-960.

**keep — не снимать surface MVP-ограничение.**  
Граница подтверждена и spec, и узкими тестовыми assertions. Наличие callable entity transport не является разрешением показать его в UI.

**question — сохранить существующий вопрос владельцам MOS-960/backend/product.**  
Какой согласованный серверный контекст связывает выбранную сущность с проверяемой версией и фактическими данными стенда? Это уже известная зависимость C08–C09, а не новая модель или выбранный протокол. Вопрос не блокирует фиксацию найденного implementation gap.

**new — не требуется.**  
Новый самостоятельный issue или политика не обоснованы. Найденное относится к существующему MOS-960; MOS-962 остаётся владельцем синхронизации.

Ничего не опубликовано и не записано в очередь: её ведёт parent.

## SHA-256 входов

Полные файлы хешированы локально; диапазоны выше обозначают семантически прочитанные участки. Хеш полного файла не означает аудит всех его сценариев.

Префикс `A/` = `openspec/changes/reconcile-control-center-backlog/audit/`.

```text
4f6db63102f34912d4c50dc39d9f936635054dc805ddfbcf086414d5fe268cb8  A/sources/jira-sandbox-details/r1/content.json
685bd0e3937a50ba0ace7e9b810f5ac9a12a67e7d67e9b61b47f8e6fbe51daaf  A/sources/jira-sandbox-details/r1/metadata.json
6e3360b9ab2bc2399ccdd63ac08aa13c7df3c1823b48435eebca321bbb3448f4  A/reports/SCENARIO-MOS-960.md
d61d7ac2993d584660d00dcf51284fbd54600e037fec2f8432dcc8ebfa41b45f  A/reviews/R-SCENARIO-MOS-960.md
6cce36bc512cc01cd7ef1552fa29676fd385243a37e14720352a0de27564632f  A/decisions.md
bfed26db7f9865a85e19e0cdfbeb0b92fc7b2b16999be3dac4d1cb92bd5eaf4e  A/work-items/WAVE-D093-LOCAL-EIGHT.md
c756d932bb442ad34cda9636ba6917e12e3fab57d949dd904432debe993332b3  app/routes/sandbox.tsx
e39b58ae268a8ef3eb906326cba5cb4e7fc21dba97589fec52090b6b745c5e69  app/pages/placeholder/ui/placeholder-page.tsx
bf50517737722446a5999e1c09ba3b2c603cc837cee23a8ab871e6418c29a21d  app/shared/config/constants/application-routes.constants.ts
de83617451674b4906697a3270c037ae7ff15b3abc0db710c76b3611cb9fd5f6  app/entities/skill/api/skill-details-client.ts
de2e6b1c1ef909dd21d0744f64d3371a456bb4c8997b658e98cfe2abdfe4ac05  app/entities/surface/api/surface-registry-client.ts
0529edf144c1ad74d58119ba7c327bcb29c3886f3335e5a8ebf4407caa038465  app/entities/surface/model/use-surface-lifecycle-mutation.ts
4fe9c6b6edf3e19fbf3ca781e49176c2e660208b5dc63b3824a4ffd946ad9c75  app/entities/surface/model/use-surface-mutation-controller.test.tsx
a69b0948e9aecf25618b1db83c27d06a804885b61ab8848e55f84d260f1558a5  app/widgets/skill-details/ui/skill-details.test.tsx
5ff98d3c6e74786075c2060fb207171f56be28a70a9802e13d0fb6e50b9def3c  app/widgets/surface-details/ui/surface-details.test.tsx
c0b4e5e78802df7c61015822330d4b7f9f510ee254a5efd9686177607dfc2463  app/widgets/navigation/ui/application-navigation.test.tsx
675265a0ba98b45f1d659f6048fe97f2e590a0597d7eda304cdcfe9854ebdd91  openspec/specs/surface-lifecycle-publication/spec.md
```

Content hash Jira совпал с сохранённым `/sha256` metadata.

## Ограничения

- Исторический cutoff Jira — сбор 16.10.2026, последнее сохранённое обновление MOS-960 — 15.10.2026. Более позднее состояние issue неизвестно. Custom fields и тела вложений не собирались.
- Текущие локальные файлы идентифицированы хешами. Заявленный work-item baseline HEAD независимо не проверялся; git/index не исследовались.
- Нет deployment evidence: не проверены сервер, rollout, доступность endpoint, реальные permissions, сессия, изоляция стенда или соответствие загруженной конфигурации.
- Не запускались тесты, сборка, сеть, browser или API. Assertions в файлах — описание покрытия, а не пройденный результат.
- Проектные файлы, отчёты, ledgers и публикационная очередь tools не изменялись. Полный отчёт возвращён для сохранения runtime в назначенный `audit/reports/IMPL-MOS-960.md`.