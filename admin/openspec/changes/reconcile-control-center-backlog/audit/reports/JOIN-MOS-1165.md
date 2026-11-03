# JOIN-MOS-1165 — ограниченная сверка

## Результат

**Частичное статическое подтверждение реализации; исправление геометрического дефекта не доказано.** Точное требование о позиционировании списка отсутствует в проверенном OpenSpec owner. Рекомендация: отдельное минимальное corrective planning, без изменения исторических ledger, main/archive specs и feature-checkboxes.

HEAD: `bc0d9800f25a90989b9c73c76f91996f8300f1d3`. `git status --short` не вывел изменений.

Здесь `A` — `openspec/changes/reconcile-control-center-backlog/audit`.

## 1. Источник и атомарное требование

Основной источник: `A/sources/jira-subtasks/r1/content.json#/items/12`, строки 248–266:

- key: `MOS-1165`;
- parent: `MOS-709`;
- тип: `Dev-bug (sub-task)`;
- статус сохранённого снимка: `Backlog`;
- updated: `2026-10-09T15:06:55.903+0800`.

| ID | Требование / контекст | Точный locator |
|---|---|---|
| R1 | При раскрытии списка «Владелец поверхности» на шаге «Ответственные» добавления поверхности список не должен смещаться относительно поля выбора. | `/items/12/description`: шаги 1–2, ФР и ОР «Смещения нет» |
| C1 | В сохранённом описании дефект наблюдался на `https://mobile-a-tech.mos.ru/tsam-panel/`. Это исторический контекст, не результат текущей проверки. | `/items/12/description`, вводная строка |
| E1 | Приложен файл `2.png`, attachment ID `832288`, размер 49032. Доступны только метаданные. | `/items/12/attachments/0` |

Не выделяю искусственных отдельных требований о ширине, точном отступе, направлении раскрытия или выбранном элементе: источник их не задаёт.

Связанные сохранённые требования: `A/sources/wiki-241080065-readable/r1/content.txt:17–23` описывают четырёхшаговый мастер и назначение ответственных; строка 51 — пошаговую регистрацию. Они подтверждают контекст, но не определяют геометрию popup.

`metadata.json` revision 1 фиксирует получение `2026-10-16T11:23:01.951Z`, отсутствие скачанных вложений, комментариев и custom acceptance fields. Поэтому направление и величина исторического смещения неизвестны.

## 2. API: применимость и пределы

**Для R1 изменение бизнес-API неприменимо.** Это требование к расположению UI, а не к данным или серверной операции.

Текущий целевой контрол — выбор команды-владельца, не поиск ответственного бизнес-пользователя:

- `app/features/surface-registration/ui/steps/responsibles-step.tsx:19–26` подключает `OwnerTeamField`;
- `owner-team-field.tsx:10–35` использует `teamId`, список `teams` и отображение `team.name`.

Нельзя подменять этот дефект проверкой `responsible.product` или `responsible.connection`: это соседние поля. API-правила этих назначений в main spec не доказывают правильного позиционирования владельца.

Полная сверка контрактов teams/create-surface не выполнялась: для атомарного R1 она не нужна. Новые endpoints, поля, auth-модель или серверная валидация из MOS-1165 не следуют.

## 3. OpenSpec coverage

**Текущий предметный owner:** `openspec/specs/surface-registration/spec.md`.

Проверенные требования main spec:

- `Responsible assignments use business user identifiers`;
- `Creation supports an atomic optional configuration`;
- `Rejections are distinct from unknown creation outcomes`;
- `Empty production catalog explains registration blocking and recovery`.

Ни одно явно не задаёт отсутствие смещения списка команды-владельца.

Проверены соответствующие архивные delta:

1. `openspec/changes/archive/2026-10-15-update-control-center-api-contracts/specs/surface-registration/spec.md` — первые три требования, без геометрии списка.
2. `openspec/changes/archive/2026-10-16-fix-existing-scenarios-test-contour/specs/surface-registration/spec.md` — пустой prod-каталог, не MOS-1165.

Отдельного текущего delta owner для R1 в выполненном поиске не обнаружено.

`A/coverage.json` имеет `complete:false`, `acceptedEvidenceThrough:"D-089"`. Источник nested population — `reports/G2-JIRA-MEMBER-JOINS.md`; строка 308 содержит MOS-1165 со статусом `U`. В `/members/overlays` отдельного перехода MOS-1165 нет. `U` означает неразрешённый аналитический join, а не отсутствие реализации. Настоящий отчёт сам по себе не изменяет population.

## 4. Код и тесты: expected / observed / unknown

### Expected

Открытый список «Владелец поверхности» остаётся привязанным к соответствующему полю без описанного нежелательного смещения.

### Observed

`app/features/surface-registration/ui/steps/owner-team-field.tsx:14–35`:

- поле занимает `md:col-span-2`;
- trigger имеет `className="w-full"`;
- используется общий `SelectContent` без локальных параметров позиционирования.

`app/shared/ui/select.tsx:55–95`:

- используется `@base-ui/react/select`;
- popup размещается через `Portal` и `Positioner`;
- defaults: `side='bottom'`, `sideOffset=4`, `align='center'`, `alignOffset=0`, `alignItemWithTrigger=true`;
- ширина popup задаётся `w-(--anchor-width)`, также присутствует `min-w-36`.

Это доказательство использования штатного позиционирования и связи ширины с anchor, **не доказательство отсутствия дефекта**. В частности, `alignItemWithTrigger=true` нельзя автоматически объявить ни исправлением, ни причиной исторического смещения.

Статически прочитаны релевантные части `app/widgets/surface-registration/ui/tests/surface-registration.test.tsx`:

- строки 100–102 проверяют сохранение выбранной команды в combobox;
- helper `selectOwnerTeam`, строки 855–858, открывает нужный combobox и выбирает «ДИТ, портал» в listbox.

Эти проверки подтверждают наличие сценария открытия/выбора в тестовом коде, но не проверяют координаты popup. Проверка соседних колонок на строках 158–170 относится к типу поверхности и доменам, поэтому не засчитывается как покрытие MOS-1165.

### Unknown

- воспроизводится ли смещение в текущем UI;
- соответствуют ли defaults Base UI исходному визуальному ожиданию;
- поведение при выбранном значении, узком viewport и ограниченном свободном месте;
- реальная геометрия и исторический вид `2.png`.

Тесты не запускались. Успешность тестов, runtime и deployment не утверждается.

## 5. Findings и минимальная коррекция плана

### F1 — отсутствует точное требование в OpenSpec

**Рекомендация: new**, после независимого review создать узкий change-кандидат `fix-surface-owner-dropdown-alignment`:

- `proposal.md`: только MOS-1165, шаг «Ответственные», поле «Владелец поверхности»; API и соседние поля вне scope.
- `specs/surface-registration/spec.md`: ADDED requirement, например `Owner selector remains anchored to its field`.
  - Нормативный текст: «При раскрытии списка “Владелец поверхности” на шаге “Ответственные” мастер регистрации SHALL сохранять привязку списка к полю выбора без нежелательного смещения относительно поля».
  - Scenario: открытие списка владельца → список остаётся привязанным к этому полю.
- `tasks.md`: незавершённые задачи:
  1. Уточнить геометрическую причину и критерий проверки по доступному свидетельству; отсутствие изображения явно сохранить.
  2. При подтверждённой необходимости исправить позиционирование адресно в `OwnerTeamField`, не менять глобальный Select без проверки остальных потребителей.
  3. Добавить component regression для выбранной политики позиционирования и граничного состояния; отдельно отметить, что DOM/component assertions не подтверждают пиксельную геометрию.

**Question:** если требуется точное восстановление исторического визуального результата, необходимы локально доступное вложение `832288` либо отдельно согласованный критерий. Это не основание сейчас скачивать вложение или запускать browser-тесты.

### F2 — доказательства недостаточны для закрытия дефекта

**Keep:** текущую реализацию не менять на основании одной статической гипотезы. Сохранить существующие main/archive specs и все исторические checkbox/ledger.

После review допустимо лишь отдельное additive evidence-решение о частичном join; не объявлять исправление, приёмку или deployment.

## 6. SHA256 ключевых входов

Пути ниже однозначно соответствуют прочитанным файлам; `A` определён выше.

| Вход | SHA256 |
|---|---|
| `A/work-items/WAVE-D090-EIGHT.md` | `98e63a056d15acd94e6bcf2fa78065bc5ea4ebf9ddc2bcf13cfaf2b3900f871b` |
| `A/sources/jira-subtasks/r1/content.json` | `c4c86b024d8e0ef30bd5234eb13ee2a9a85d4fa29eeb9cb2a37c024d75d3652e` |
| `A/sources/jira-subtasks/r1/metadata.json` | `d9c0f1c289e6f2d675b5cc07994956fa039e846919b08726d637f027279cfe20` |
| `A/coverage.json` | `e93adb588725fb39b55f278270ad33e4d7e9da8ac73ee4620d4c0293740d791b` |
| `A/sources/wiki-241080065-readable/r1/content.txt` | `265c282d02fa14d85ad28b13a4fb5dd5d2e73573d2c2b7d652311c369acd7f25` |
| `openspec/specs/surface-registration/spec.md` | `31928d907bfff75eca61d2efe176879e3c7f4d3e0029dbe6bb97258b8d00f9a5` |
| Архивная delta `2026-10-15-update-control-center-api-contracts/specs/surface-registration/spec.md` | `20183114e812bea2bd54cd2c4f54b49277f9c485bb68fbbe9032d948c3a1e047` |
| Архивная delta `2026-10-16-fix-existing-scenarios-test-contour/specs/surface-registration/spec.md` | `cbf6470a59c038b83faefe9df58aac4b3f935d5ee6ae2e2cfcaebdab4c9b8ed7` |
| `app/features/surface-registration/ui/steps/owner-team-field.tsx` | `210c9a4166bfac16fb6e06ad77f696c7a2f4ab5d0bd0157bd10f12512dcc9058` |
| `app/features/surface-registration/ui/steps/responsibles-step.tsx` | `9369174cce262cc69eddfb9984c0f67702dd854c16bd2b74f660459b2527ba4b` |
| `app/shared/ui/select.tsx` | `87858971de8d53f575fcea4c524c2dfd9009ff5ea0a31103f6ca9cfc90d12e04` |
| `app/widgets/surface-registration/ui/tests/surface-registration.test.tsx` | `c50563fcaf2ce4ea6844a38c8805675922c3169a1ecc2ebdfc0d655ea4976c53` |

## Ограничения процедуры

Read-only, только MOS-1165. Без сети, браузера, делегации, выполнения тестов и изменений проекта. Первоначальное чтение coverage по неверному пути завершилось `FileNotFoundError`; затем штатным поиском найден и прочитан `A/coverage.json`. Недоступность изображения известна из metadata, изображение не заменялось предположениями.