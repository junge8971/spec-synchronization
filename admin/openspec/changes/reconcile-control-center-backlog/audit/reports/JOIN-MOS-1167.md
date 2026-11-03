# JOIN-MOS-1167 — адреса после ввода доменов

## Итог и границы

**Обнаружен узкий UI/spec gap:** на первом шаге регистрации нет отдельной строки с введёнными адресами. Нормализованные домены вычисляются, но показываются отдельным списком только на итоговом шаге. Это не подтверждает исполнение MOS-1167. **Не следует восстанавливать генерацию channel_id или кода подключения:** источник требует появления адресов, а не синтетических серверных данных.

HEAD, проверенный `git rev-parse HEAD`: `bc0d9800f25a90989b9c73c76f91996f8300f1d3`.
Обозначения: `A = openspec/changes/reconcile-control-center-backlog/audit`; `F = app/features/surface-registration`.
Только локальное статическое чтение и этот отчёт; без сети, браузера, тестового выполнения, git mutations и изменений ledger/checkboxes. Deployment и исправление на историческом контуре не подтверждены.

## 1. Точное сохранённое требование

Основной источник **прочитан по телу**, не выведен из заголовка: `A/sources/jira-subtasks/r1/content.json#/items/14`, строки 285–310; описание — строка 293.

- key `MOS-1167`, parent `MOS-709`, Dev-bug (sub-task), Backlog, updated `2026-10-09T15:08:08.485+0800`.
- Контекст: `https://mobile-a-tech.mos.ru/tsam-panel` — исторический адрес воспроизведения, не проверенная сейчас среда.
- Шаги: «Перейти в раздел добавления поверхности»; «Ввести валидные данные в поле Домены».
- ФР: «Строчка с адресами с введенными данными не появляется».
- ОР: «Адреса появляются».

**R1 (единственное атомарное требование):** после ввода валидных данных в «Домены» в добавлении поверхности появляется строка адресов, отражающая введённые данные. Источник не требует сначала завершить мастер или создать поверхность.

Дополнительные точные локаторы:

| Свидетельство | Локатор | Значение и предел |
|---|---|---|
| Связь с родителем | `A/sources/jira-member-index/r1/content.json#/items/118/subtasks/4`, строки 1032–1036 | Точный ключ и статус, не самостоятельное описание |
| Вложения | `...jira-subtasks/r1/content.json#/items/14/attachments/0` и `/1` | `832324 / 4.png / 68070 bytes`, `832323 / 5.png / 59585 bytes`; только metadata |
| Provenance | `...jira-subtasks/r1/metadata.json` | retrievedAt `2026-10-16T11:23:01.951Z`; вложения не скачаны, comments/custom acceptance fields отсутствуют |
| Соседний контекст, не замена R1 | `A/sources/wiki-241080065-readable/r1/content.txt:18,49,70` | Ввод доменов в мастере; домены и channelId в обзоре; channelId присваивается платформой |

Тело задачи доступно: **body gap отсутствует**. Неизвестны визуальный образец строки, точное форматирование, момент обновления onChange/onBlur, подпись и поведение при невалидном вводе. Из названия «адреса канала» нельзя вывести необходимость генерировать channel_id, endpoint или embed code.

## 2. Owner и прежняя evidence

Текущий owner: `openspec/specs/surface-registration/spec.md:9–80`. Его требования относятся к ответственным, атомарному созданию, отказам/неизвестному исходу и пустому prod-каталогу; отдельного отображения адресов при вводе нет.

Прочитанные архивные delta:

- `openspec/changes/archive/2026-10-15-update-control-center-api-contracts/specs/surface-registration/spec.md:7–56` — ответственные, configuration и ошибки, не R1.
- `openspec/changes/archive/2026-10-16-fix-existing-scenarios-test-contour/specs/surface-registration/spec.md:3–19` — пустой prod-каталог, не R1.

По локальному поиску файлов `**/*surface-registration*/spec.md` отдельная активная delta этого owner не найдена. Граница смежного owner: `openspec/specs/surface-overview-connection/spec.md:9–21` требует серверные значения после GET и запрещает синтез кода/channel_id; это не покрытие первого шага регистрации.

Повторно использованы inventory/member joins, но не как новое функциональное покрытие: `A/reports/JIRA-MOS-783.md:52–68` фиксирует S[14] и отсутствие изображений; `A/reports/G2-JIRA-MEMBER-JOINS.md:310` содержит MOS-1167 → `I(118)/subtasks/4 → S(14)`, состояние `U/UN`. `A/coverage.json` сохраняет `complete:false`, `acceptedEvidenceThrough:D-089`; отдельного overlay MOS-1167 нет. `U` означает незавершённую аналитическую связку, не отсутствие кода. Покрытие всего модуля MOS-783 и соседних MOS-1164/1165 не засчитывается за R1. Настоящий отчёт не меняет population.

## 3. API и текущая реализация

### Expected

На шаге ввода доменов появляется отдельное представление адресов из введённых данных. Оно не должно выдавать локальный ввод за подтверждённые занятость домена, серверный канал или сохранённую конфигурацию.

### Observed

| Участок | Наблюдение |
|---|---|
| `F/ui/steps/surface-details-step.tsx:12,58–73` | Компонент получает только `form`; поле «Домены» — textarea. Следом выводятся только статические «Занятость доменов не проверена» и «Идентификатор канала назначается сервером после создания». Нет строки адресов, map/join или другого зависимого от значения вывода |
| `F/model/use-surface-registration.ts:41–60,73` | `useWatch` формирует draft; `parseDomains(draft.domains)` вычисляет актуальный список |
| `F/model/parse-domains.ts:1–18` | Разделение по пробелам/переносам/запятым/`;`, lowercase, удаление http(s) и конечных `/`, удаление пустых и дублей. Это нормализация, не доказательство DNS-доступности |
| `F/ui/surface-registration-step-content.tsx:11–12,35–43` | Details получает только form; domains передаются Review |
| `F/ui/steps/review-step.tsx:18–22` | Только итоговый шаг выводит `domains.join(', ')` и серверное назначение идентификатора. Этот поздний вывод не заменяет R1 |
| `F/model/to-create-surface-request.ts:11–25` | В request уходят нормализованные domains, channel_id не генерируется |

Релевантный локальный API-контракт: `app/shared/api/schema.d.ts:2771–2806` — `CreateSurfaceRequest.domains: string[]`, ответ создания содержит `id`; `:3355–3368` — сохранённая карточка содержит `domains: string[]` и `channel_id: string | null`. Никакого требования выводить адресную строку на этапе набора эти DTO не задают. Для отражения уже введённых доменов **новый API не нужен**; сохранение существующей модели POST/GET обязательно. Полный endpoint-аудит не выполнялся и отсутствие preview API во всей системе не утверждается.

### Статически прочитанные тесты

- `app/widgets/surface-registration/ui/tests/surface-registration.test.tsx:158–170`: соседние колонки type/domains — layout, не адресная строка.
- Там же `:173–190`, `uses local domain validation without searching the registry or generating a channel`: после ввода mos.ru проверяет две статические подсказки, отсутствие запроса реестра и переход к ответственным. **Не проверяет появления адресов.** Сохранять этот запрет генерации канала, не ослаблять тест ради R1.
- `F/model/tests/surface-registration.test.ts:41–54`: нормализация/дедупликация и отклонение пустого нормализованного списка; `:68–86`: нормализованные domains в request. Это полезные нижележащие проверки, но не UI-регрессия MOS-1167.

### Unknown

Runtime не проверен; изображения 4.png/5.png недоступны локально по provenance. Нельзя подтвердить историческую геометрию/точный дизайн, статус backend/deployment или окончательное продуктовое значение слова «адреса» за пределами отражения введённых данных. Наличие textarea со значением само по себе не считается появлением описанной отдельной строки.

## 4. Минимальные findings

1. **new (кандидат после независимого review):** узкий corrective change `show-surface-domain-preview` с `proposal.md`, `specs/surface-registration/spec.md`, `tasks.md`. ADDED requirement: при вводе валидных доменов первый шаг SHALL показывать адреса из текущего ввода, отдельно от неподтверждённых серверных данных. Не менять исторические main/archive. Tasks оставить незавершёнными: адресный UI-вывод; component regression на появление нескольких доменов и обновление/очистку строки; сохранение отсутствия запросов проверки занятости и генерации канала. При согласовании объединения с соседними дефектами поверхности использовать один owner без дублирующих полных MODIFIED блоков.
2. **keep:** текущие `parseDomains`, request mapping и серверное назначение channel_id; не вводить новый API, автоматическую проверку занятости, ссылки на выдуманные endpoints, новый канал или код подключения. Existing tests не ослаблять. Для реализации переиспользовать существующий derivation/form-watch, не создавать отдельную независимую модель доменов.
3. **question (ограниченная):** нужен ли точный исторический визуальный формат? Тогда требуется локальное изображение `832324/832323` или согласованный критерий. Без этого не утверждать точные URL-схему, расположение, кликабельность и подпись. Это не разрешение внешней загрузки и не препятствие фиксации минимального R1.

`update` существующего активного плана не предлагается: точный активный delta owner не обнаружен. Решение о публикации/состоянии evidence принимает parent после review; автоматического закрытия MOS-1167 нет.

## 5. SHA256 ключевых прочитанных входов

Хеши вычислены локально по байтам (не только переписаны из metadata).

| Путь | SHA256 |
|---|---|
| `A/work-items/WAVE-D090-EIGHT.md` | `98e63a056d15acd94e6bcf2fa78065bc5ea4ebf9ddc2bcf13cfaf2b3900f871b` |
| `A/work-items/WAVE-D090-REVIEW-NEXT.md` | `fdf9ed7a57cc427bf9feb58639fe976fb2f76fb1bd9082c0f1626649cfdfcc72` |
| `A/sources/jira-subtasks/r1/content.json` | `c4c86b024d8e0ef30bd5234eb13ee2a9a85d4fa29eeb9cb2a37c024d75d3652e` |
| `A/sources/jira-subtasks/r1/metadata.json` | `d9c0f1c289e6f2d675b5cc07994956fa039e846919b08726d637f027279cfe20` |
| `A/sources/jira-member-index/r1/content.json` | `dba6cffa66e0aef23e9ef34c4a52215a5c02d31e7da1dca87888e821198b8043` |
| `A/coverage.json` | `e93adb588725fb39b55f278270ad33e4d7e9da8ac73ee4620d4c0293740d791b` |
| `A/reports/JIRA-MOS-783.md` | `4088bb978c718cee5104e570f42ab0b99191a4035f5f9752a80e098153b56354` |
| `A/reports/G2-JIRA-MEMBER-JOINS.md` | `dc9b199c2a9500b2ff1857de1feaec9282e8130fa1b78720f551913907618b44` |
| `A/sources/wiki-241080065-readable/r1/content.txt` | `265c282d02fa14d85ad28b13a4fb5dd5d2e73573d2c2b7d652311c369acd7f25` |
| `openspec/specs/surface-registration/spec.md` | `31928d907bfff75eca61d2efe176879e3c7f4d3e0029dbe6bb97258b8d00f9a5` |
| `openspec/specs/surface-overview-connection/spec.md` | `51f9dc1a1d7b92ccdb059b7fda0117bf6c898378fa9a9fe185c7e2045044d193` |
| `openspec/changes/archive/2026-10-15-update-control-center-api-contracts/specs/surface-registration/spec.md` | `20183114e812bea2bd54cd2c4f54b49277f9c485bb68fbbe9032d948c3a1e047` |
| `openspec/changes/archive/2026-10-16-fix-existing-scenarios-test-contour/specs/surface-registration/spec.md` | `cbf6470a59c038b83faefe9df58aac4b3f935d5ee6ae2e2cfcaebdab4c9b8ed7` |
| `app/shared/api/schema.d.ts` | `394a55fc0bd646a9a3c81dace045d89f53505fc40bc4cb0902cb1492b638092d` |
| `F/ui/steps/surface-details-step.tsx` | `22d151070d49763e756e8f9bb4bde445b1d0fd448256a15d4be2468b30962953` |
| `F/ui/steps/review-step.tsx` | `1467c7a855a642a9a7b98e9781e68b363d594e192782ef356621853962a38cfe` |
| `F/ui/surface-registration-step-content.tsx` | `43455d674c1049bb92d1a7cc07372323625cfe35e645fa35a2f915fe0718635f` |
| `F/model/use-surface-registration.ts` | `4a5ee2fcb09f6cbcdbc063653d1dbaad10956a8a54fa7944a61865857adaa8c4` |
| `F/model/parse-domains.ts` | `5f5c20e127f98fb8296456420f3ba0644d5296f5a1f2077945c5d725785dbcd2` |
| `F/model/to-create-surface-request.ts` | `102b6382781f52b006d69d020849c818759d87a034d1a02c057efc1f214df564` |
| `F/model/tests/surface-registration.test.ts` | `3186703cc7c35ee464516fc8883c20576efe4361b45a1aeaa84c565505250f31` |
| `app/widgets/surface-registration/ui/tests/surface-registration.test.tsx` | `c50563fcaf2ce4ea6844a38c8805675922c3169a1ecc2ebdfc0d655ea4976c53` |

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Прочитано точное тело MOS-1167 /items/14; R1 сопоставлен с owner, DTO, первым и итоговым шагами и конкретными тестами; unknown и минимальные рекомендации выделены."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/JOIN-MOS-1167.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"git rev-parse HEAD","result":"passed","summary":"HEAD соответствует контракту"},
    {"command":"python: exact-key JSON extraction and hashlib.sha256 of listed inputs","result":"passed","summary":"Найден /items/14; хеши вычислены"},
    {"command":"tests/build/lint/typecheck/browser","result":"not-run","summary":"Запрещены заданием; выполнено только статическое чтение"}
  ],
  "validationOutput": ["Первый шаг не содержит динамической строки адресов; итоговый шаг содержит domains.join(', ')."],
  "residualRisks": ["Изображения не сохранены; точный визуальный формат неизвестен.","Runtime, deployment и успешность тестов не проверены."],
  "noStagedFiles": true,
  "diffSummary": "Только новый отчёт; код, specs, исторические ledgers и checkbox не изменены.",
  "reviewFindings": ["Нужны независимое review и решение parent о corrective planning; закрытие дефекта не заявлено."],
  "manualNotes": "Read-only анализ точного member. Один поисковый запрос к предполагаемому surface-management owner вернул Path not found; актуальный surface-registration owner затем найден и прочитан. Staging не выполнялся; состояние чужого index не проверялось."
}
```
