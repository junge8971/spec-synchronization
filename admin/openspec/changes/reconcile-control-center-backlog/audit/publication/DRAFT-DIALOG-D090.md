# DRAFT-DIALOG-D090

**Назначение отчёта:** `/home/user/my/work/codesrc/projects/CAM/tsam-admin-front/openspec/changes/reconcile-control-center-backlog/audit/publication/DRAFT-DIALOG-D090.md`

**Статус: draft / publication-held.** Ни scaffold, ни файлы change не созданы. Ниже — полное предлагаемое содержимое четырёх артефактов `fix-dialog-registry-presentation-and-reset`.

Основания: **D-090**, обязательные ограничения `R-D090-EIGHT`, freshness hold из **D-091**, задание `WAVE-D092-REVIEW-AND-DRAFTS / DRAFT-DIALOG-D090`. Отдельные названия changes из исходных JOIN-отчётов заменены согласованным единым owner. MOS-1422 не включён в corrective scope.

Прочитаны `.agents/skills/openspec-propose/SKILL.md`, `.agents/skills/openspec-update-change/SKILL.md` и `openspec/config.yaml`. Read-only `openspec context --json` подтвердил текущий корень. Создание native scaffold, получение его artifact instructions, публикация и независимая приёмка остаются за parent. Этот draft не является самоприёмкой или разрешением на implementation.

## 1. Baselines и источники

Ниже `A` означает `openspec/changes/reconcile-control-center-backlog/audit`. SHA256 вычислены заново по локальным байтам.

### Основные baselines

| Файл | SHA256 |
|---|---|
| `openspec/specs/dialog-registry/spec.md` | `ef9e52b7dba2ff4f0fa1dd1a9fa3d7cfaa78890277c376d70ed0301423bf6f83` |
| `openspec/specs/dialog-selection-builder/spec.md` | `87d9ad1687832a1f1eb54a69b65d168cfe04a94fdc5bed1f95ea25983afc8ca6` |
| `A/decisions.md` | `fa7cffedb00f4d481efa2b523e8f1a1b4991b2750022c823c30c5370ab5cf945` |
| `A/work-items/WAVE-D092-REVIEW-AND-DRAFTS.md` | `a397d1cfc2441cb0c4d44183878917b5dd5e80bbe292ca0220871afed68451ee` |
| `A/reviews/R-D090-EIGHT.md` | `2df7b2655f9fb3ffac901f2b8a946e336579e0ab72a50be49a0223a6d8342a6f` |
| `A/reports/JOIN-MOS-1411.md` | `a5641af49c067fb64358ea1a23b8f39405aaa2268946bb328f2bf9e1eb7879f9` |
| `A/reports/JOIN-MOS-1412.md` | `b037676ea37fbcd839a2a5e776b4bf038a2011996af1c369723fd98d2f61bc9e` |
| `A/reports/JOIN-MOS-1414.md` | `325aaae186c680ced84f29d7b96ad957e234aa717895105c2751b5a6a9db7cd4` |
| `A/reports/JOIN-MOS-1419.md` | `c99a68e4e50e9241ba6fe795d34c6e6f2a21dd643e15b8467a9db728faa08745` |

Точный исходный блок `Registry represents server rows faithfully`, от его `### Requirement` до следующего requirement, включая завершающую пустую строку: `19e49512a8bbef7aaa16288958d6284406e82b320fd975ef2406910d01db7526`.

Предлагаемый MODIFIED блок сохраняет исходный нормативный абзац и оба исходных сценария **дословно**, затем добавляет уточнения и сценарии. Остальные main requirements не заменяются.

### Источники требований

Локаторы основаны на четырёх принятых JOIN-отчётах и независимом review; повторная внешняя проверка не выполнялась.

| Источник | Использование |
|---|---|
| `A/sources/jira-subtasks/r1/content.json#/items/2/description` | MOS-1411: исходное скрытие, общий сброс, повторное скрытие |
| Тот же файл, `/items/3/description` | MOS-1412: красная точка перед первой репликой |
| Тот же файл, `/items/4/description` | MOS-1414: серверная длительность и «и идёт» |
| Тот же файл, `/items/5/description` | MOS-1419: прочерк при null rating |
| `A/sources/wiki-243776365/r1/content.json`, `bodyView`, СПС-25 и «Сценарий 1. Сброс отбора» | Пять частей сбрасываемого отбора, условная видимость |
| Тот же источник, СПС-32 и состав строки | Независимое отображение сбоя |
| `A/sources/wiki-241085439/r1/content.json`, `bodyView`, §§2.3, 2.5.1, 2.7 | `has_failure`, `ended_at`, `duration_sec`, `operator_rating` |
| Тот же источник, §7, §8.6, §8.11 | Ограничения происхождения серверных признаков и длительности; не клиентская реконструкция |
| `A/sources/api-live/r1/content.json`, search POST | Существующий selection/reset contract |
| `A/sources/api-live/r2/content.json`, search POST и `components.schemas.DialogListItemResponse.properties.operator_rating` | Nullable rating в существующем ответе |
| Main `dialog-registry`: `Quick filter application is visibly explicit` | Сохранение pending quick draft, validation и явного submit |
| Main `dialog-selection-builder`: `Draft changes require explicit application` | Сохранение редактора, отдельной очистки draft и общего сброса |

| Сохранённый источник | SHA256 content / metadata |
|---|---|
| `jira-subtasks/r1` | `c4c86b024d8e0ef30bd5234eb13ee2a9a85d4fa29eeb9cb2a37c024d75d3652e` / `d9c0f1c289e6f2d675b5cc07994956fa039e846919b08726d637f027279cfe20` |
| `wiki-241085439/r1` | `974ea35aaf44b9ec7c14c573ba58bdf7ed55397a9ca47d62b37fb39d9886f8bc` / `dcaab775172b7e615dfae64184d719f8403cff1fb304650ba21e1532ce577b7d` |
| `wiki-243776365/r1` | `2f659b5423fa7203dcd4f70743e59aabfb571452144394621091ff2cd58cab55` / `fc250c2633f28f6a8f408835145a59aa4cb8612606b40cb8bf79cf088ea256b8` |
| `api-live/r1` | `549f70b756ee1c29982b176b75faa8a665f9083956bae96dcfbae85e3d3dff06` / `3d92a2024209edecf98eaa1095e40a565611c9eb6ccc4de312ed900165b9f8ff` |
| `api-live/r2` | `ab5527772e16273222bad8a5f4a35ffe1de4e612630e1111e2f5612db4996993` / `444c7b65941db4af36d1ffe305fd04499a44d6d9c81b9a25be15dc6061d521ba` |

### Проверенные implementation baselines

| Файл | SHA256 |
|---|---|
| `app/pages/dialogs/ui/dialog-filters.tsx` | `72d95c6383ec7ffc36a7fa638f8fc3b2fa562008bea94e0c9c0fd13d6fb0f66d` |
| `app/pages/dialogs/ui/dialog-registry.tsx` | `5e487284416e43ae82a20fe43a20546bb327e44e8c8f0f95e77ba427b52aa801` |
| `app/pages/dialogs/model/quick-filter-key.ts` | `e78ec79cd89688b765ffcece2189b25309359db59ff3de29dba26aeb0e399757` |
| `app/pages/dialogs/ui/dialog-table/dialog-table-row.tsx` | `3096df76cead86dad46f13be6cbde70de0a2c0d009c0842f82087f89ad985de3` |
| `app/entities/dialog/ui/dialog-operator-rating.tsx` | `089bf7705ca41e9117cffea1c219fb3c6171169608761ba8f01415845395ad04` |

Дополнительно прочитаны релевантные тесты `dialogs-page.test.tsx`, `dialog-operator-rating.test.tsx` и композиция `app/features/dialog-selection/ui/dialog-selection.tsx`. Тесты не запускались.

## 2. Полные предлагаемые артефакты

### `openspec/changes/fix-dialog-registry-presentation-and-reset/proposal.md`

```markdown
## Why

Принятый анализ D-090 и независимое review R-D090-EIGHT установили четыре ограниченных расхождения реестра диалогов с сохранёнными требованиями MOS-1411, MOS-1412, MOS-1414 и MOS-1419: общий сброс виден в исходном пустом состоянии, сбой обозначен бейджем вместо красной точки перед обращением, длительность незавершённого диалога не дополнена словами «и идёт», а null-оценка показана текстом «Нет оценки» вместо прочерка.

Три изменения строки относятся к одному существующему requirement. Единый change предотвращает конфликтующие полные замены этого блока.

Пакет остаётся planning draft: D-091 фиксирует изменение timestamps четырёх исходных Jira-задач. Публикация требует отдельного сохранённого freshness comparison и независимого review; прежняя аналитическая приёмка не подтверждает актуальность новых редакций или delivery.

## What Changes

- Уточнить один полный requirement представления строки: доступно обозначенная красная точка перед первой репликой при has_failure=true; серверный снимок duration_sec с «и идёт» только при ended_at=null; прочерк в ячейке оценки при operator_rating=null.
- Добавить отдельный requirement видимости общего сброса для активного применённого отбора и неприменённых быстрых изменений.
- Сохранить очистку всех пяти частей отбора, pending quick draft, явное применение, валидацию, обработку ошибок, доступность и существующее поведение редактора сложных условий.
- Добавить unit/component-регрессии положительных и граничных случаев.

Не входят: новый API, изменения DTO/auth, клиентский таймер или polling, карточка диалога, исправления сортировки, поверхности, новый policy для исключительно неприменённого сложного draft. MOS-1422 остаётся функциональным planning no-op, а не пятой корректировкой.

## Capabilities

### New Capabilities

Нет.

### Modified Capabilities

- `dialog-registry`: точное представление серверной строки и условная видимость общего сброса без изменения существующей семантики применения отбора.

`dialog-selection-builder` остаётся неизменным владельцем поведения сложного draft; его требования сохраняются без дублирующей delta.

## Impact

Основные места будущих изменений: `app/pages/dialogs/ui/dialog-table/dialog-table-row.tsx`, `app/pages/dialogs/ui/dialog-filters.tsx` и адресные unit/component-тесты. Существующая нормализация `quickFilterKey` используется для быстрых фильтров; применённая группа условий учитывается отдельно.

Null-представление общей `DialogOperatorRating` и её потребителей карточки не меняется. Существующий search API, cursor identity, безопасный текст, basename-aware переходы и числовые оценки сохраняются. Новые зависимости не нужны.

Источники: `reconcile-control-center-backlog/audit/decisions.md` (D-090, D-091), `reviews/R-D090-EIGHT.md`, `reports/JOIN-MOS-{1411,1412,1414,1419}.md`; исходные Jira `/items/2–5/description`, wiki-243776365 СПС-25/СПС-32 и wiki-241085439 §§2.3/2.5.1/2.7. Отчёты находятся под тем же audit root.

Main specs, архивы, исторические ledgers и feature-checkboxes этим planning-пакетом не изменяются. Browser/E2E без отдельного разрешения запрещены.
```

### `openspec/changes/fix-dialog-registry-presentation-and-reset/design.md`

```markdown
## Context

D-090 принимает четыре статических join как основание одного corrective owner, а R-D090-EIGHT задаёт обязательные границы интеграции. Текущая строка уже получает все нужные поля из принятого API. Она отображает бейдж «Сбой» под обращением, форматирует duration_sec без признака продолжения и передаёт null в общий DialogOperatorRating, который показывает «Нет оценки».

DialogFilters уже различает pending быстрые изменения через quickFilterKey, но кнопку общего сброса рендерит безусловно. Сброс очищает форму и применённый selection; DialogRegistry перемонтирует редактор условий через editorVersion. Сам редактор сохраняет собственный draft до применения.

D-091 сохраняет publication hold: timestamps четырёх Jira-задач изменились. Этот design не разрешает публикацию до сохранённого freshness comparison и независимого review.

## Goals / Non-Goals

Goals:
- Исправить только MOS-1411, MOS-1412, MOS-1414 и MOS-1419.
- Сохранить полный существующий row requirement и все его сценарии в одной MODIFIED delta.
- Сохранить явное применение быстрых и сложных условий, validation, ошибки, доступность и cursor identity.
- Проверить исправления unit/component-тестами.

Non-Goals:
- Изменение API/schema, auth, карточки, сортировки, поверхностей или backend-алгоритмов.
- Клиентские часы, пересчёт длительности или polling.
- Новый продуктовый policy для exclusively unapplied complex-condition draft.
- Переписывание main/archive или завершение audit/feature-checkboxes.
- Browser/E2E без отдельного разрешения.

## Decisions

### 1. Один владелец и один полный MODIFIED row requirement

В `specs/dialog-registry/spec.md` сохраняются дословно исходный нормативный абзац и сценарии `Unfinished and unrated dialog` и `Multiple participants and failure`. Новые положения уточняют их, не заменяя шесть бизнес-колонок, поля ответа, навыки/remainder, независимые признаки, авторизационную пометку, safe text и basename-aware ссылку.

Reset оформляется одним ADDED requirement. Существующие `Quick filter application is visibly explicit` и `Draft changes require explicit application` не заменяются и не дублируются в других delta.

### 2. Предикат видимости общего сброса

Для согласованных состояний учитываются два независимых основания:
- применённый отбор отличается от исходного по q, period, channel_ids, skill_ids либо содержит применённые условия;
- быстрый draft отличается от применённых быстрых значений.

Быструю часть следует сравнивать существующим quickFilterKey: trim q, нормализация отсутствующих/пустых IDs, порядка и дублей, all_time и custom dates. Это сохраняет уже существующее определение pending changes. quickFilterKey не содержит condition_group, поэтому применённая непустая группа проверяется отдельно.

Одного hasPendingChanges недостаточно: применённый активный отбор должен сбрасываться и без pending edits. Одного сравнения applied quick filters с default недостаточно: оно теряет группу условий и pending quick draft.

Обратный или неполный custom period остаётся draft и не обязан проходить validation для доступности сброса. Сброс остаётся type=button, не submit; невалидный быстрый draft можно очистить без предварительного применения. Также остаётся доступным сброс при pending возврате быстрых контролов к default, пока применённый отбор ещё активен.

Начальное пустое состояние без изменений скрывает кнопку; после общего сброса она скрыта. Loading/error справочников не меняет эти основания.

Существующий reset path сохраняется: очистить форму, применить initialDialogSelection и сбросить редактор через существующий callback. Все пять частей снимаются одним действием, без предварительной ручной очистки группы. Существующее поведение сортировки при сбросе не переопределяется.

### 3. Неприменённый сложный draft не получает нового policy

Видимость общего сброса в состоянии, где изменён только неприменённый draft сложных условий, остаётся явным нерешённым вопросом источников. Этот change не определяет для него новое обязательное visible/hidden поведение и не добавляет критерий приёмки одной из трактовок.

Не поднимать private complex draft в registry ради нового предиката и не менять lifecycle редактора. Сохранить его применение, закрытие без применения, отдельную очистку draft и существующую обработку общего сброса. Если реализация потребует нового решения именно для complex-only состояния, вынести вопрос на согласование, а не выводить ответ из MOS-1411.

### 4. Сбой — серверный boolean и доступная красная точка

В строке реестра точка располагается перед DialogText первой реплики. Она зависит только от has_failure; навыки и has_operator остаются независимыми. Сбой нельзя реконструировать из сообщений или маршрута.

Красный цвет не является единственным доступным обозначением: сохранить текстовое доступное имя сбоя. Не фиксировать неподтверждённые pixel size, hex color или offsets. Сохранить безопасную обработку текста, truncation только представления и basename-aware Link.

### 5. Длительность — снимок без клиентского времени

Оставить форматирование duration_sec в минуты/секунды; при ended_at=null добавить «и идёт» в ту же ячейку. При ненулевом ended_at суффикс отсутствует. Ноль обрабатывается как допустимая длительность. Новое серверное значение меняет представление, но течение клиентского времени само по себе его не меняет.

Отдельная колонка завершения сохраняет «не завершён». Таймеры, polling и изменения карточки не нужны.

### 6. Null rating исправляется только в реестре

Ячейка реестра при operator_rating=null выводит прочерк без звёзд и без видимого «Нет оценки», независимо от ended_at и has_operator. Конкретный Unicode-символ источниками не закреплён.

Для чисел 1–5 сохраняется существующий DialogOperatorRating с его доступным именем и звёздами. Общий null branch компонента и его тест сохраняются для остальных потребителей, включая карточку; глобальная замена была бы расширением scope.

## Risks / Trade-offs

- Дублирующие MODIFIED deltas могли бы потерять соседние изменения; используется один полный блок, а перед публикацией и sync требуется проверка baseline.
- Component-тесты подтверждают структуру, условность и accessibility semantics, но не являются browser/geometric доказательством.
- Исторические Jira attachments представлены metadata; из них нельзя выводить размеры точки или дополнительные визуальные требования.
- Complex-only draft policy остаётся нерешённым и не должен появиться в implementation по умолчанию.
- Сохранённые источники не доказывают актуальность deployment или реальную работу backend.

## Migration Plan

Изменений данных и API нет. После freshness comparison, native scaffold и независимой приёмки planning-пакета реализация выполняется отдельным apply workflow. Откат ограничивается представлением реестра и адресными тестами.

При будущей синхронизации заменить только полный row requirement и добавить reset requirement; остальные main requirements и dialog-selection-builder сохранить. При изменившемся baseline сначала выполнить lossless rebase и повторное review.

## Validation Strategy

Unit/component-проверки:
- начальное и post-reset скрытие, каждый из пяти применённых критериев отдельно;
- simultaneous reset всех пяти непустых частей, не очищая группу заранее;
- pending quick draft, invalid custom draft, pending возврат к default и доступность при ошибке справочников;
- failure true/false независимо от operator, точка перед первой репликой и доступное обозначение;
- finished/unfinished duration, ноль, обновление серверного снимка без клиентского пересчёта;
- null rating при обоих состояниях завершения и operator flag, отсутствие звёзд/видимого «Нет оценки»;
- числовые рейтинги 1–5, доступность и неизменное null-представление общего компонента;
- сохранение safe text, basename-aware ссылки, explicit apply, ошибок и cursor-поведения.

При реализации выполнить yarn typecheck, yarn lint без предупреждений, yarn test и yarn format:check. API/build checks нужны только при соответствующих изменениях; расширение текущего scope ради них не планируется. Browser/E2E не запускать без отдельного разрешения.
```

### `openspec/changes/fix-dialog-registry-presentation-and-reset/tasks.md`

```markdown
## 1. Presentation corrections

- [ ] 1.1 В строке реестра заменить представление сбоя доступно обозначенной красной точкой перед первой репликой, сохранив независимость has_failure/has_operator/skills, safe text и basename-aware ссылку.
- [ ] 1.2 Дополнить серверный duration_sec словами «и идёт» только при ended_at=null, сохранив нулевую длительность и отдельную колонку завершения; не добавлять таймер или polling.
- [ ] 1.3 Добавить registry-local прочерк при operator_rating=null без звёзд и видимого «Нет оценки»; сохранить DialogOperatorRating для 1–5 и неизменное поведение карточки.

## 2. Reset visibility

- [ ] 2.1 Условно показывать общий сброс по активному применённому отбору либо pending quick draft, используя существующую нормализацию быстрых фильтров и отдельный учёт применённых условий.
- [ ] 2.2 Сохранить сброс всех пяти частей, очистку quick draft и существующий reset редактора; обеспечить сброс invalid quick draft без submit и не менять complex-only unapplied draft policy.
- [ ] 2.3 Сохранить явное применение, validation, обработку ошибок справочников и поиска, доступность управления и cursor identity.

## 3. Unit and component regressions

- [ ] 3.1 Проверить отсутствие сброса в исходном пустом состоянии и после сброса; проверить каждый применённый критерий отдельно, включая condition_group при пустых быстрых фильтрах.
- [ ] 3.2 Проверить одним действием сброс одновременно непустых q, period, channel_ids, skill_ids и condition_group без предварительной очистки группы.
- [ ] 3.3 Проверить pending quick edits, обратный/неполный custom period, pending возврат к default и reset при ошибке справочников; сохранить проверки keyboard submit и отсутствия преждевременного изменения выдачи.
- [ ] 3.4 Проверить failure true/false при независимом operator flag, порядок точки перед первой репликой и доступное обозначение, сохранив проверки навыков, авторизации, safe text и ссылки.
- [ ] 3.5 Проверить finished/unfinished duration, включая ноль и обновление серверного снимка; подтвердить отсутствие клиентского пересчёта.
- [ ] 3.6 Проверить null rating при обоих состояниях завершения и operator flag, отсутствие звёзд/видимого «Нет оценки» в ячейке; сохранить проверки чисел 1–5 и accessibility общего компонента, не меняя его null-контракт.
- [ ] 3.7 Сохранить регрессии request errors, continuation/retry и cursor reset без расширения corrective scope на сортировку.

## 4. Validation and review

- [ ] 4.1 Выполнить yarn typecheck, yarn lint без предупреждений, yarn test и yarn format:check; отдельно зафиксировать passed/failed/not-run и внешние причины сбоев.
- [ ] 4.2 Просмотреть diff на потерю существующих требований и поведения, случайные файлы и выход за scope; не изменять main/archive, audit ledgers и feature-checkboxes вне согласованного lifecycle.
- [ ] 4.3 Подтвердить отсутствие API/schema/auth/card/surface изменений, новых зависимостей и browser/E2E-проверок; при неожиданной необходимости API/build изменений получить согласование scope и выполнить соответствующие проверки.
```

### `openspec/changes/fix-dialog-registry-presentation-and-reset/specs/dialog-registry/spec.md`

```markdown
## MODIFIED Requirements

### Requirement: Registry represents server rows faithfully

Реестр SHALL показывать шесть колонок: обращение/участники, начало, завершение, поверхность, оценка работы оператора, длительность. Строка SHALL использовать chat_id, first_user_message, skills, has_operator, has_failure, user_authorization, started_at, ended_at, duration_sec, channel_id, channel_name, operator_rating. Первые два навыка и число остальных SHALL отображаться без потери независимых признаков оператора и сбоя. Пометка «без авторизации» SHALL соответствовать unauthorized и authorized_in_dialog. Переход SHALL адресовать карточку по chat_id с сохранением UI basename.

При has_failure=true реестр SHALL показывать красную точку перед текстом первой реплики пользователя. Индикатор SHALL иметь доступное текстовое обозначение сбоя и не зависеть от навыков или участия оператора. При has_failure=false индикатор сбоя MUST NOT отображаться.

Ячейка длительности SHALL показывать форматированный серверный duration_sec. При ended_at=null она SHALL дополнять длительность словами «и идёт»; при ненулевом ended_at эти слова MUST NOT отображаться. Длительность SHALL оставаться снимком ответа сервера, включая нулевое значение; UI MUST NOT увеличивать её по клиентским часам. Отдельная колонка завершения SHALL сохранять «не завершён» при ended_at=null.

При operator_rating=null ячейка оценки реестра SHALL показывать прочерк вместо видимого текста «Нет оценки», без звёзд и без подмены отсутствующей оценки нулём, независимо от ended_at и has_operator. Числовые оценки 1–5 SHALL сохранять существующее доступное представление. Это правило null-представления SHALL применяться только к реестру и MUST NOT изменять представление оценки в карточке диалога.

#### Scenario: Unfinished and unrated dialog

- **WHEN** ended_at и operator_rating равны null
- **THEN** строка показывает «не завершён» и отсутствие оценки, а не фиктивную дату и нулевую оценку

#### Scenario: Multiple participants and failure

- **WHEN** диалог содержит пять навыков, оператора и сбой
- **THEN** видны первые два навыка, «ещё 3», пометка оператора и доступно обозначенный сбой; текст обращения безопасно сокращён только в представлении

#### Scenario: Failure indicator precedes the first message

- **WHEN** сервер передаёт has_failure=true независимо от наличия оператора и навыков
- **THEN** перед текстом первой реплики показана красная точка с доступным обозначением сбоя, а признаки оператора и навыков сохраняются независимо

#### Scenario: No failure indicator for a successful dialog

- **WHEN** сервер передаёт has_failure=false независимо от has_operator
- **THEN** индикатор сбоя отсутствует, а представление оператора и навыков определяется их собственными полями

#### Scenario: Unfinished duration remains a server snapshot

- **WHEN** ended_at=null и сервер передаёт duration_sec, в том числе 0
- **THEN** ячейка длительности показывает форматированный снимок и «и идёт», не увеличивая значение с течением клиентского времени; колонка завершения показывает «не завершён»

#### Scenario: Finished duration has no continuation suffix

- **WHEN** ended_at содержит дату и сервер передаёт duration_sec, в том числе 0
- **THEN** ячейка показывает форматированную серверную длительность без «и идёт», а колонка завершения сохраняет серверную дату

#### Scenario: A new response updates the duration snapshot

- **WHEN** новый серверный ответ содержит изменённый duration_sec для незавершённого диалога
- **THEN** реестр показывает новый снимок с «и идёт», не вычисляя длительность по клиентским часам

#### Scenario: Null rating is a registry dash

- **WHEN** operator_rating=null у завершённого или незавершённого диалога независимо от has_operator
- **THEN** ячейка оценки реестра показывает прочерк без звёзд и без видимого «Нет оценки», а null-представление карточки диалога не меняется

#### Scenario: Numeric operator ratings remain accessible

- **WHEN** operator_rating содержит целое значение от 1 до 5
- **THEN** ячейка сохраняет соответствующую числовому значению оценку и её доступное обозначение, не заменяя её прочерком

## ADDED Requirements

### Requirement: Global reset visibility preserves applied selection and quick drafts

Общий сброс SHALL быть доступен в строке фильтров при активном применённом отборе по q, периоду, поверхностям, навыкам или группе условий, а также при неприменённых изменениях быстрых фильтров. Исходное пустое состояние без изменений SHALL скрывать общий сброс. После общего сброса, когда применённый отбор и быстрый draft возвращены к исходному состоянию, кнопка SHALL быть скрыта.

Доступность сброса неприменённых быстрых изменений SHALL сохраняться и для невалидного custom period; сброс MUST NOT требовать предварительного применения draft. Общий сброс SHALL очищать q, возвращать период к all_time, очищать поверхности, навыки и группу условий, а также быстрый draft, сохраняя существующие правила явного применения и сброса редактора.

Этот requirement сохраняет `Quick filter application is visibly explicit` и `Draft changes require explicit application`. Он не задаёт новую политику видимости для состояния, отличающегося только неприменённым draft сложных условий.

#### Scenario: Initial empty selection

- **WHEN** реестр открыт с исходным пустым отбором, периодом all_time и без изменений draft
- **THEN** общий сброс не отображается

#### Scenario: Each applied selection part can be reset

- **WHEN** применён только один активный критерий: q, отличный от all_time период, непустые поверхности, непустые навыки либо непустая группа условий
- **THEN** общий сброс доступен, даже если быстрый draft совпадает с применёнными быстрыми значениями

#### Scenario: Reset all five active selection parts together

- **WHEN** q, период, поверхности, навыки и группа условий одновременно применены и пользователь нажимает общий сброс без предварительной очистки группы
- **THEN** одним действием очищаются все пять частей, период возвращается к all_time, очищается быстрый draft и сохраняется существующий сброс редактора; поиск использует сброшенный отбор без прежнего cursor

#### Scenario: Reset becomes hidden after completion

- **WHEN** общий сброс возвратил применённый отбор и draft к исходному состоянию
- **THEN** кнопка скрыта и сообщение о неприменённых быстрых изменениях отсутствует

#### Scenario: Pending quick changes remain resettable

- **WHEN** пользователь меняет быстрые фильтры без применения, в том числе при исходном пустом применённом отборе
- **THEN** общий сброс доступен; до применения или сброса выдача, total и экспорт продолжают использовать прежний применённый отбор

#### Scenario: Invalid quick period can be reset without applying

- **WHEN** быстрый draft содержит неполный или обратный custom period и пользователь нажимает общий сброс
- **THEN** draft очищается без предварительного валидного submit, все части применённого отбора возвращаются к исходным значениям и сохраняются существующие правила поиска со сброшенным отбором

#### Scenario: Pending return to defaults does not hide an active reset

- **WHEN** применённый быстрый отбор активен, а пользователь без submit вернул быстрые контролы к исходным значениям
- **THEN** общий сброс остаётся доступен и очищает также ещё действующий применённый отбор
```

## 3. Границы приёмки и остаточные риски

- Полный исходный MODIFIED requirement сохранён без потерь; reset добавляется отдельно. Main и archive не изменены.
- Complex-only unapplied draft не получил новой политики или тестового требования visible/hidden.
- **Публикация заблокирована freshness gate D-091** до сохранённого сравнения изменившихся источников и независимого review этого draft.
- Native scaffold/schema validation не выполнялись; parent должен сверить артефакты с native instructions перед публикацией.
- Проверки кода, сеть, browser/E2E и изменения файлов не выполнялись. Документ не подтверждает delivery, deployment или работу backend.