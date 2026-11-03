# JOIN-MOS-911 — выбор продовых навыков и параметры поверхности

## Результат и границы

**Предметный статический join выполнен только для MOS-911.** Основные требования имеют текущего владельца, реализацию и содержательные unit/component assertions. Новый самостоятельный product-change по проверенной части не обоснован; кандидат — **keep** существующего поведения и additive evidence для parent review.

Это не приёмка реализации, успешное выполнение тестов, публикация или закрытие Jira. Parent самостоятельно решает eligibility и возможный переход исторического U в аналитическое P. Исторические строки и соседние members не изменяются.

Обозначения:

- `A` = `openspec/changes/reconcile-control-center-backlog/audit`
- `F` = `app/features/surface-skill-selection`
- `S` = `openspec/specs/surface-skill-selection/spec.md`

## 1. Точный источник

`A/sources/jira-surface-details-d095/r1/content.json#/items/6`:

- key: **MOS-911**;
- summary: «[FE][Поверхности] Реализовать выбор сценариев и параметры навыков поверхности»;
- status: `Ready for test`;
- updated: `2026-10-20T14:30:48.953+0800`;
- точное item retrievedAt: **`2026-10-20T16:56:26.462Z`**;
- collection retrievedAt: `2026-10-20T16:56:26.589Z` — отдельный timestamp;
- `attachments=[]`;
- `comments.total=3`, сохранены все три комментария.

### Атомы требований

| Источник | Expected |
|---|---|
| `/items/6/description`, первый абзац | Продовые навыки по доменам; индивидуальное включение, включение домена, количество выбранных и массовый выбор. |
| Там же, второй абзац | Поля параметров из `key/title/type/required/default/options`. |
| Там же, третий абзац | Учитывать исчезновение или недоступность ранее выбранного навыка. |
| `/items/6/comments/items/2`, id `1122997` | Автор утверждает реализацию в регистрации и редактировании; описывает сохранение параметров между шагами, блокировку невалидных значений, POST, PUT enabled-skills, причины недоступности, retry и явное снятие. Это утверждение и инструкция тестирования, **не результат тестового запуска**. |
| `/items/6/comments/items/1`, id `1122089` | Упоминание MR16 и ветки MOS-911. MR не открывался; merge/deployment этим не установлены. |
| `/items/6/comments/items/0`, id `1114073` | Оценка «4-5», не acceptance evidence. |

Description прямо ссылается на wiki **241082009** и **241097511**. `parent:null` не отменяет подтверждённое parent-пакетом членство MOS783. Самостоятельно членство и ledger eligibility не переопределялись.

## 2. Предшествующие решения и владельцы

Перед предметной инспекцией использованы решения D-090/091/093, reviews `RECON-MOS-959.md`, `RECON-MOS-959-CONTRACT.md`, `R-D091-RECOVERY.md`, отчёт `JOIN-MOS-1166.md` и `publication/DRAFT-SURFACE-D091.md`.

Сохраняются следующие границы:

- **D-004/005:** configurator отложен; versioned wiki/API расхождения не разрешены выбором «более нового» источника. Сохранение навыков не разрешает hidden/default `/configuration` PUT.
- **D-090/091:** MOS1166 — отдельное визуальное ограничение описательного текста; MOS1167 — отражение доменного ввода. Они не входят в новую ownership-запись MOS911. Geometry MOS1110/1165 и target MOS1164 также не присваиваются MOS911.
- **D-093:** статус навыка `sandbox` в проверке выбора не является разрешением sandbox workflow поверхности.

Прочитаны proposal/design/tasks/spec обоих архивных владельцев:

1. `openspec/changes/archive/2026-09-30-mos-911-surface-skill-selection/`
   — первоначальная общая feature, параметры и обе интеграции; историческое ограничение отсутствия prod-фильтра.
2. `openspec/changes/archive/2026-10-02-mos-911-prod-skill-selection/`
   — последующая prod-фильтрация и уточнённая классификация недоступности.

Текущий `S` уже содержит результат второго владельца. Старую фразу «prod-фильтра нет» нельзя переносить в текущую оценку. Архивные checked tasks и описанные прежние проверки остаются историческими записями, а не выполненными в этом запуске командами.

## 3. Expected / observed / unknown

| Обязательство | Observed: код и assertions | Unknown / ограничение |
|---|---|---|
| Полный prod-каталог | `F/model/use-surface-skill-selection.ts`, `useSurfaceSkillSelection`: запрос `useSkillsCatalogQuery('prod', allowed)` и защитная фильтрация статуса. `app/entities/skill/api/skill-registry-client.ts:54–94`: status передаётся каждой странице `getAllSkills`. Client test `:240–312` проверяет offsets, status на обеих страницах и rejection при отказе промежуточной страницы. Owner: `S`, **Contract-backed skill catalog**. | Backend-фильтрация и согласованность пагинации в deployment не проверены. Цикл заканчивается также при пустой странице; описанные assertions не доказывают поведение при противоречивом успешном ответе «пустые items, но total ещё не достигнут». |
| Доменный/индивидуальный/массовый выбор | `F/ui/surface-skill-selection-editor.tsx`: prod-группы, общий счётчик, обе массовые кнопки. `F/model/skill-selection.ts`, `toggleDomainSelection`, `enableAllSkills`, `disableAllSkills`, `getDomainSelectionState`: объединение без дубликатов, сохранение проблемных ID при включении всех, очистка выбора без очистки параметров. Model tests `:31–70`; editor tests `:34–86`: mixed state, клавиатура, независимость групп, исключение non-prod. Owner: **Domain and bulk selection**. | Component tests читаются как assertions; фактическая браузерная доступность/геометрия не измерены. |
| Схема и defaults | `skill-selection.ts`, `normalizeSkillParameterSchema`, `normalizeSkillParameter`, `initializeSkillParameters`, `normalizeDefaultValue`: только select; неизвестный тип/дубли ключей/required без options дают проблему; defaults однократные, числовое значение преобразуется в строку и проверяется по options. `F/ui/skill-parameter-field.tsx`: title, required marker, options, ошибка и устаревшее значение. Model tests `:72–105,199–270`; editor `:52–66,139–155`. Owner: **Schema-driven parameters**. | Это текущая frontend-семантика согласованных specs, не гарантия серверной нормализации. Не добавляются новые типы полей. |
| Принадлежность и сохранность параметров | `skill-selection.ts`: значения и initialized keys по skill ID; переключения не очищают map. Hook не переинициализирует уже отмеченные поля defaults. Model tests `:31–45,72–79`; registration test `:399–435` проверяет независимые одинаковые ключи двух навыков и POST. Owner: **Parameter ownership and draft preservation**. | Исчерпывающая проверка всех гонок фоновых ответов не выполнялась. |
| Исчезновение/недоступность | `validateSelectedSkill`: 404 → not-found; другие ошибки → detail-error; non-prod сохраняет фактический status; detail=prod при отсутствии в каталоге → catalog-mismatch, не «удалён». `prepareEnabledSkills` возвращает пустой write payload при невалидном результате. Model tests `:107–197`; editor `:157–253`: причины, retry и явное снятие. Owner: **Revalidation and missing skills**. | Отсутствие в prod-списке не доказывает удаление. Surface-specific eligibility не появляется из prod/zones/auth-полей. |
| Изменение схемы и явное исправление | `validateSelectedSkill` выдаёт issue для неизвестного сохранённого ключа; `validateParameterValues` отвергает option вне схемы; `removeSkillParameterValue` — отдельное действие. Editor test `:255–272` проверяет видимое старое значение и вызов удаления. | Нельзя молча считать частичный `validateSkillSelection.payload` пригодным к записи: отправку разрешает valid gate; финальный prepare очищает payload при ошибке. |
| Повторная проверка перед записью | Hook `prepare`: refetch полного каталога и выбранных details, отказ при свежей ошибке даже с cached data, preparing lock. Model tests `:159–197`: prod→sandbox, возврат prod с сохранением значения, свежая ошибка. Surface details tests `:837–936`: нет PUT при смене статуса/ошибке каталога; retry сохраняет параметры. | Между GET и записью остаётся гонка; атомарная eligibility-проверка или expected skill version не установлены. |
| Регистрация и редактирование | `app/widgets/surface-registration/ui/surface-registration.tsx:15–75`: общий controller живёт выше шагов, prepare передаётся регистрации, editor блокируется во время preparation/lock. Registration tests `:399–501`: POST с параметрами двух навыков, один POST на двойное событие, отсутствие POST при отказе каталога. `app/widgets/surface-details/ui/surface-details.tsx`: инициализация из server enabled_skills. `.../surface-details/model/use-surface-details-operations.ts:64–105`: valid gate, PUT только enabled_skills, server response как новая база, ошибка без фиктивного успеха. Details tests `:777–936`: точный payload, отсутствие configuration, пустой PUT после явного снятия, retry. Owner: **Registration and existing surface persistence**. | Это не повторный аудит регистрации MOS958, lifecycle MOS914 или overview MOS913. Реальная persistence и повторное открытие deployed приложения не проверены. |

## 4. API и связанные источники

### Текущий локальный контракт

`docs/api/contracts/openapi.json`:

- `/paths/~1api~1control~1api~1skills~1v1~1skills/get/parameters` — status, limit, offset;
- `/paths/~1api~1control~1api~1skills~1v1~1skills~1{skill_id}/get` — detail;
- `/components/schemas/SkillConnectionParameterSchema` — key/title/type/required/default/options; default допускает string/integer/null;
- `/components/schemas/UpdateSurfaceEnabledSkillsRequest` — required `enabled_skills`;
- `/paths/~1api~1control~1api~1surfaces~1v1~1surfaces~1{surface_id}~1enabled-skills/put` — отдельное сохранение состава.

По проверенному списку paths **available-skills отсутствует**. Это факт локального snapshot, не доказательство отсутствия произвольного endpoint в deployment.

### Историческая wiki

`A/sources/wiki-241097511/r2/content.json#/bodyView`, раздел **1.5 Подключение навыка**, таблица **SurfaceParameter**; удобное представление:

`A/sources/wiki-241097511-readable/r1/readable-text.txt:197–212`.

Таблица подтверждает шесть полей, select и string/integer/null default. Строка 212 ссылается на historical `/available-skills`; текущий main spec явно запрещает изобретать этот endpoint. Метаданные derivation связывают readable-r1 именно с исходным **wiki r2**, page version 6, captured `2026-10-16T12:37:03.295Z`.

Для wiki241082009 использованы уже принятые точные разборы `RECON-MOS-959-CONTRACT.md`: source `sources/wiki-241082009/r2/content.json#/bodyView`, §2.5 описывает combined configuration/skills PUT. Это сохранённое расхождение с текущим split API; оно не повод менять MOS911 transport или активировать configurator. Повторная полная сверка MOS959 не выполнялась.

## 5. Ограниченные кандидаты для parent

1. **Keep:** существующие `surface-skill-selection` requirements, prod-каталог, schema-driven select/defaults, независимый draft, причины недоступности и preflight.
2. **Update — только audit evidence:** добавить точный MOS911 body/comment join к текущему owner. Не переписывать прежний U ledger и не переносить coverage MOS1166/1167.
3. **New:** самостоятельный product-change по проверенным обязательствам не предлагается.
4. **Question / optional evidence strengthening:** при необходимости отдельно проверить успешную, но внутренне противоречивую пагинацию с пустой промежуточной страницей и оставшимся total. Здесь не установлено ни такое backend-поведение, ни обязательный новый алгоритм.
5. **Сохранённые вопросы:** backend enforcement, deployed behavior и гонка GET→write остаются неизвестны; ни новый eligibility API, ни policy выбора источника не предлагаются.

## 6. SHA-256 входов

Хеши вычислены локально по байтам файлов.

| Путь | SHA-256 |
|---|---|
| `A/sources/jira-surface-details-d095/r1/content.json` | `7f03f2bbb04798d98bab8bc12a1c4b16511d26112f56da4378f5e0ae5796f62a` |
| `A/sources/jira-surface-details-d095/r1/metadata.json` | `508b6ea6333bda12d26e3d828ceeca071ecf5fd9ee2042406ecf1b992f4d931a` |
| `A/sources/wiki-241097511/r2/content.json` | `710e56e84b2d228d705dfe9b7fce1d8a0c38a0dbcce17b2ff9cf5b1240cc5f47` |
| `A/sources/wiki-241097511-readable/r1/readable-text.txt` | `c6dd8857060fa4e87a7170fb604486d12d03a8e74d1ac24c4704554eba67b2df` |
| `docs/api/contracts/openapi.json` | `c6e13858e1cfc2574c6830356ddfa0fc4dfbd38db43c4b19e0faab5ef9f432f7` |
| `S` | `e27eb8b354e4370da3519b5387cff5369a2f083e6c3be05f82d8631746c19ee0` |
| `F/model/skill-selection.ts` | `4a6a56ae3458ff83097da24f61aab56fce53ed4d82fbb22fa920ecc24ab4bbb4` |
| `F/model/use-surface-skill-selection.ts` | `5b4a48a4812df614113454873b54823fed452fefd5807d894ed90efe199697f9` |
| `F/model/tests/skill-selection.test.ts` | `5033721db89254e98589cac303f1b464d1551ac58c436a71044522df141fe004` |
| `F/ui/surface-skill-selection-editor.test.tsx` | `223c5241a669d93aebdcc756b902e67b6969a24fa275eec0ca9b1645d3af7c9e` |
| `app/entities/skill/api/skill-registry-client.ts` | `fe22d8076a52c22ea245853b2bbe3f7103a1f515776920a6ecf76b6a6fcd5969` |
| `app/widgets/surface-details/ui/surface-details.test.tsx` | `5ff98d3c6e74786075c2060fb207171f56be28a70a9802e13d0fb6e50b9def3c` |
| `app/widgets/surface-registration/ui/tests/surface-registration.test.tsx` | `c50563fcaf2ce4ea6844a38c8805675922c3169a1ecc2ebdfc0d655ea4976c53` |

## 7. Ограничения и журнал проверки

- No network/browser/business API, tests/build/lint/typecheck/format, Git mutations, config changes или nested agents.
- Файлы не записывались; итог передаётся runtime для authoritative output path.
- HEAD из задания — `bc0d9800f25a90989b9c73c76f91996f8300f1d3`; самостоятельно через Git не подтверждался.
- Fresh Jira packet не обновляет автоматически wiki/API snapshots и остальные publication gates.
- Custom fields не собраны; MR не traversed. Статус и комментарий о реализации не доказывают delivery.
- Были ошибки разведки путей: предполагаемый `app/widgets/surface-details/model/...` отсутствовал; фактический owner найден через imports/search в `ui/surface-details/model/`. Первый hash-batch ошибочно предполагал wiki241097511 **r1/content.json**; r1 содержит исторический access-result, а readable metadata указывает на существующий r2. Ошибки сохранены как provenance, не представлены успешными командами. Это не отсутствие обязательного fresh MOS911 source и не смена режима/model/source fallback.
- Один объединённый предварительный вывод reviews был обрезан; существенные reviews и source locators затем прочитаны адресно. Полный независимый повтор соседних accepted audits не заявляется.
- No mandatory-source blocker выявлен для данного bounded join. Acceptance, очередь и публикация остаются исключительно у parent.