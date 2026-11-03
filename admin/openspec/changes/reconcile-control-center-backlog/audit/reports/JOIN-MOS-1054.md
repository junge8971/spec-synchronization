# JOIN-MOS-1054 — мобильный автоскролл документации

## Результат

**keep**: требование уже принадлежит `documentation-search`, текущий код содержит адресную реализацию, component-тест содержит точное ожидание прокрутки к началу выбранной статьи. Новое изменение продукта не обосновано. Это статическое сопоставление именно MOS-1054, не принятие всего модуля документации и не подтверждение исправления на контуре.

HEAD из контракта: `bc0d9800f25a90989b9c73c76f91996f8300f1d3` (самостоятельно не проверялся). `A` ниже означает `openspec/changes/reconcile-control-center-backlog/audit`; `O` — `openspec/changes/archive/2026-10-13-mos-906-documentation-search-url`; `W` — `app/widgets/documentation/ui`.

## Источник и атомарное требование

- `A/sources/jira-subtasks/r1/content.json:312–320`, `$.items[15]`: точный key `MOS-1054`, parent `MOS-705`, тип Dev-bug (sub-task), сохранённый статус CLOSED, updated `2026-10-09T21:44:15.111+0800`.
- **Первичное тело**, `$.items[15].description`, строка 319: «1. Перейти в раздел документации с моб. устройства; 2. Выбрать статью из списка; ФР: Автоскролла к началу статьи нет; ОР: Автоскролл есть». Это не вывод из заголовка. Указанный в теле `https://mobile-a-tech.mos.ru/tsam-panel` — исторический контур воспроизведения, не проверенный адрес текущего развёртывания.
- **R1054-1:** после выбора статьи из списка документации на мобильном устройстве выполняется автоматическая прокрутка к началу статьи. Отдельных требований к API, длительности анимации, breakpoint или повторному нажатию на уже выбранную статью тело не задаёт.
- `A/sources/jira-member-index/r1/content.json:1167–1180`, `$.items[135].subtasks[0]`: подтверждает связь MOS-705 → MOS-1054. Повторное использование `A/reports/JIRA-MOS-784.md:20–37` ограничено членством и происхождением: это прежний inventory, не функциональное доказательство.
- `$.items[15].attachments[0..1]`, строки 320–335: только metadata видео 835960 (MOV) и 835961 (MP4); их содержимое не сохранено/не просмотрено. `metadata.json` сообщает retrievedAt `2026-10-16T11:23:01.951Z`, selected-field-redacted-extraction, отсутствие comments/custom acceptance fields. SHA256 содержимого совпадает с metadata. CLOSED не доказывает выполнение.

## Expected / observed / unknown

| Атом / граница | Expected | Observed | Unknown |
|---|---|---|---|
| R1054-1, ручной выбор другой статьи на мобильном | Прокрутка к началу выбранной статьи | `W/documentation-catalog.tsx:43–56`: кнопка передаёт ID. `W/handlers/documentation.handlers.ts:24–35`: смена article через штатный router без сброса прокрутки. `W/documentation.tsx:37–66`: после изменения ID при узком экране requestAnimationFrame, focus с preventScroll и `scrollIntoView({ behavior: 'smooth', block: 'start' })`. Область статьи расположена после каталога, имеет ref/id/tabIndex и scroll-mt-4 (`:76–103`). | Реальная геометрия и завершение smooth scroll на исходном устройстве/контуре, перекрытие начальной части статьи оболочкой не проверены. |
| Точное тестовое свидетельство R1054-1 | Выбор статьи приводит к вызову прокрутки к началу | `W/documentation.test.tsx:14–68`: matchMedia=true, клик «Порядок заведения навыка», выбранная статья/aria-current/aria-controls, один scrollIntoView с block:start и фокус области. Это прочитанные assertions, не результат запуска. | Тест подменяет matchMedia и scrollIntoView, не измеряет пиксели и не проверяет фактический breakpoint браузера. |
| Ограничение мобильной компоновки | Jira говорит только о мобильном устройстве | `W/constants/documentation.constants.ts:1`: max-width 1023px; layout в `documentation.tsx:76` переключается через lg. Desktop-тест `documentation.test.tsx:70–98` ожидает отсутствие scroll; первый URL-вход `:100–121` также без scroll. | Jira не задаёт численную ширину или начальный scroll offset. Это существующие решения, не извлечённые требования MOS-1054. |
| Повторный выбор уже открытой статьи | В теле не уточнён | Handler `:28–30` делает no-op; effect `documentation.tsx:38–40` требует смены ID. Текущая spec явно говорит о другой статье. | Нельзя из общей формулировки Jira объявить этот край дефектом либо потребовать новую прокрутку; видео недоступны. |

## Main / delta / archive / API

**Текущий нормативный владелец:** `openspec/specs/documentation-search/spec.md:70–87`, Requirement “Search preserves accessible interaction”, Scenario “Manual mobile selection”: ручной выбор другой статьи на узком экране фокусирует область и прокручивает её в видимую область. Ввод поиска не прокручивает, desktop и первый прямой вход также не прокручивают. Последние ограничения принадлежат текущему владельцу, а не новому расширению MOS-1054.

**Архивная цепочка:** принятый `A/reports/SPEC-G2-DOCUMENTATION-SEARCH.md` устанавливает owner через `O/proposal.md:15–20` и исходную delta `O/specs/documentation-search/spec.md:68–85`, задача `O/tasks.md:10` (2.3). В этой проверке непосредственно прочитан `O/design.md` полностью: §3, строка 39, сохраняет ручной мобильный фокус/scroll и запрещает scroll для ввода/коррекции; §2 отдельно сохраняет no-op повторного выбора. Исторический контекст design о прежнем useState не выдаётся за текущую реализацию. Прежний отчёт не проверял этот код и отмечал mobile focus/scroll как unassessed; настоящее свидетельство добавлено именно для R1054-1. Принятие ownership зафиксировано `A/decisions.md:197–201` (D-063), найдено при локальном поиске. Предполагаемый файл review `reviews/R-SPEC-G2-DOCUMENTATION-SEARCH.md` отсутствует; его содержимое не использовано.

По scoped-поиску отдельная активная delta для MOS-1054 не обнаружена; утверждение об отсутствии всех возможных пересечений не делается. `A/coverage.json:285–306` явно сохраняет P как bounded partial, ownershipOverlay documentation-search и completeLaneSetsCertified=false. Ни overlay, ни статусы не заменяют member-body join выше.

**API: неприменим к R1054-1.** Это локальный DOM/router переход, не операция backend. Main `documentation-search/spec.md:11` прямо запрещает необходимость серверного API поиска; `O/design.md:11` исключает новый API. Handler обновляет query-параметр, effect вызывает платформенные DOM API; новых endpoint/DTO/контрактов не нужно. Существующая сессия оболочки не отменяется и здесь не переоценивается. OpenAPI не читался, поскольку wire-contract для прокрутки не требуется.

## Минимальное решение

- **keep:** `documentation-search` main и существующие код/тесты; новый corrective change или изменение archive не требуется по найденным фактам.
- **update (только последующая интеграция доказательств):** parent после независимого review может добавить узкий join R1054-1 → source/spec/code/test. Не менять исторические U/P строки задним числом, не закрывать feature-checkboxes, не объявлять полное покрытие документации.
- **new:** нет обоснованного нового требования или подтверждённого дефекта.
- **question:** не блокирует keep; только если требуется доказать поведение повторного выбора той же статьи, нужны недоступные acceptance/video evidence. Сейчас не вводить такой сценарий как обязательный. Геометрия, устройства и deployed fix остаются unknown, не дефектом по умолчанию.

## SHA256 ключевых входов

Хешированы полные файлы локально; это не означает полного семантического чтения всех строк теста/реестра.

| Файл | SHA256 |
|---|---|
| `A/work-items/WAVE-D090-EIGHT.md` | `98e63a056d15acd94e6bcf2fa78065bc5ea4ebf9ddc2bcf13cfaf2b3900f871b` |
| `A/work-items/WAVE-D090-REVIEW-NEXT.md` | `fdf9ed7a57cc427bf9feb58639fe976fb2f76fb1bd9082c0f1626649cfdfcc72` |
| `A/sources/jira-subtasks/r1/content.json` | `c4c86b024d8e0ef30bd5234eb13ee2a9a85d4fa29eeb9cb2a37c024d75d3652e` |
| `A/sources/jira-subtasks/r1/metadata.json` | `d9c0f1c289e6f2d675b5cc07994956fa039e846919b08726d637f027279cfe20` |
| `A/sources/jira-member-index/r1/content.json` | `dba6cffa66e0aef23e9ef34c4a52215a5c02d31e7da1dca87888e821198b8043` |
| `A/coverage.json` | `e93adb588725fb39b55f278270ad33e4d7e9da8ac73ee4620d4c0293740d791b` |
| `A/reports/JIRA-MOS-784.md` | `5ce6b6eed5e0c9590a7b6c9e738d0bf8a2626651e91a95a54a4c9525257b1120` |
| `A/reports/SPEC-G2-DOCUMENTATION-SEARCH.md` | `003bfd5a6d6bc4b8fec05df512af67006bd4117dab87c9672749b3a982809e64` |
| `openspec/specs/documentation-search/spec.md` | `f9b88a2c524c152a4817b5e05861bb6c6e2ef3a9debf548e5b7a852135bb0c6f` |
| `O/design.md` | `849aca071ad4123c133979fbbec0c721fe3f7a71e31dd5954bc2fad0ebb5619b` |
| `W/documentation.tsx` | `727e8c68c75582aa488bbdc7f260275f66629431e5fc4b4bbd175a2a369d15a8` |
| `W/documentation.test.tsx` | `68aa39885304fc883a3121a312b8b3d32cf03e51449155b2ec07b21ecb603942` |
| `W/handlers/documentation.handlers.ts` | `abff5fd987916ece1c0de3daf532592bc0067fe63dedb3274ebe773731dffc6f` |
| `W/constants/documentation.constants.ts` | `f876ccaf09532ca06344085f7358c4e165a5ec367e01e37684ba94c351acc48e` |
| `W/documentation-catalog.tsx` | `f74df62d973fac36f65a8873fb943be8248f2b647abb044b4661f4ac96c297f4` |

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Точное тело MOS-1054 сопоставлено с main/archive owner, ручным мобильным scroll effect и адресным component assertion; unknown отделены."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/JOIN-MOS-1054.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [
    {"command":"Локальные read/find/grep и Python hashlib SHA256","result":"passed","summary":"Прочитано точное тело, вычислены 15 ключевых хешей."},
    {"command":"read reviews/R-SPEC-G2-DOCUMENTATION-SEARCH.md","result":"failed","summary":"ENOENT; не использован как доказательство, принятие ownership найдено в decisions D-063."},
    {"command":"Тесты, browser/network, build/lint/typecheck","result":"not-run","summary":"Запрещены/не требуются в read-only задании; assertions только прочитаны."}
  ],
  "validationOutput": ["R1054-1 → items[15].description → documentation-search Manual mobile selection → scrollIntoView block:start → documentation.test.tsx:14–68."],
  "residualRisks": ["Видео, comments/custom acceptance fields недоступны.","Геометрия, runtime, deployment и повторный выбор той же статьи не подтверждены; тесты не запускались."],
  "diffSummary": "Только назначенный отчёт; приложение, specs/archive, ledgers и checkbox не изменялись.",
  "reviewFindings": ["keep; новый corrective change не обоснован статическими данными."],
  "manualNotes": "Только локальное чтение и запись назначенного отчёта. Git/index не проверялся и не менялся, child fanout отсутствует. Независимое review и интеграция остаются у parent."
}
```
