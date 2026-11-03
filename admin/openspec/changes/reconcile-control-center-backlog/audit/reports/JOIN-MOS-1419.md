# JOIN-MOS-1419 — отсутствие оценки в реестре диалогов

## Результат и границы

**Обнаружено статическое несоответствие:** при `operator_rating: null` реестр выводит «Нет оценки», тогда как сохранённая подзадача требует прочерк. Существующие тесты закрепляют ошибочное представление. OpenSpec описывает отсутствие оценки, но не задаёт требуемый прочерк.

Проверен только MOS-1419, родитель MOS-1037. HEAD: `bc0d9800f25a90989b9c73c76f91996f8300f1d3`; `git status --porcelain` — пустой вывод. Изменений проекта, запусков тестов, браузера, сети и делегирования не было.

Далее `audit/` означает `openspec/changes/reconcile-control-center-backlog/audit/`.

## 1. Атомарное требование и источники

| ID | Ожидается | Локатор |
|---|---|---|
| R1 | В таблице раздела «Диалоги», в колонке «Оценка работы оператора», при `operator_rating: null` отображается прочерк вместо «Нет оценки». | `audit/sources/jira-subtasks/r1/content.json`, `$.items[5].description`, строки 109–116 |
| R1 — подтверждение контракта | `operator_rating` — целое 1–5 либо `null`; `null` означает отсутствие оценки, в реестре — прочерк. | `audit/sources/wiki-241085439/r1/content.json`, `$.bodyView`, §2.3, строка таблицы `operator_rating`; §2.7, строка «Прочерк в колонке оценки» |
| Контекст, не расширение R1 | Если оператор не участвовал, в строке списка выводится прочерк. | `audit/sources/wiki-243776365/r1/content.json`, `$.bodyView`, «Отображение оценки оператора в строке списка» |

Сохранённая Jira: Backlog, обновление `2026-10-16T18:18:36.194+0800`. Фактическое поведение «Нет оценки» в Jira — историческое сообщение автора, не результат воспроизведения этого аудита.

Требование не зависит от `ended_at` и не ограничено случаем отсутствия оператора. Не следует подменять проверку `operator_rating === null` условием `has_operator === false`. Противоречивые комбинации полей отдельно не исследовались.

## 2. API: применимость и пределы

API применим как источник значения; нового endpoint или изменения payload для R1 не требуется.

- Сохранённый контракт wiki-241085439, revision 1, версия страницы **15**, связывает представление прочерка с `operator_rating = null`.
- Сохранённый `audit/sources/api-live/r2/content.json` содержит POST `/api/control/api/dialogs/v1/dialogs/search`.
- JSON locator `$.components.schemas.DialogListItemResponse.properties.operator_rating`: `anyOf(integer, null)`. Поле входит в `required`.
- Эта OpenAPI-схема не задаёт текст UI и не содержит диапазона 1–5; диапазон указан в сохранённом бизнес-контракте.
- `app/entities/dialog/api/dialog-client.ts:14–27` принимает `null`, а числовую оценку валидирует как целое 1–5. `searchDialogs`, строки 48–55, использует `/dialogs/v1/dialogs/search`.
- `app/shared/api/schema.d.ts:2394` также допускает `number | null`.

**Вывод:** доступного контракта достаточно для исправления отображения. Ответы реально работающего backend, свежесть внешней публикации и deployment не проверены. Отсутствующее поле и `null` не объявляются эквивалентными.

## 3. OpenSpec и учёт покрытия

**Текущий владелец:** `openspec/specs/dialog-registry/spec.md`, requirement `Registry represents server rows faithfully`, строки 18–25.

Сценарий `Unfinished and unrated dialog` требует «отсутствие оценки», а не нулевую оценку, но:

1. не фиксирует прочерк;
2. объединяет `operator_rating: null` с `ended_at: null`, хотя R1 применим и к завершённому диалогу.

Архивный owner `openspec/changes/archive/2026-10-05-mos-1037-dialog-registry/specs/dialog-registry/spec.md:16–23` содержит ту же недостаточно точную формулировку. Архив `2026-10-16-fix-existing-scenarios-test-contour/specs/dialog-registry/spec.md` добавляет требования быстрых фильтров, не исправление отсутствующей оценки.

Прямых активных `changes/*/specs/dialog-registry/spec.md` при локальном поиске не найдено.

`audit/coverage.json` имеет `acceptedEvidenceThrough: D-089`, `complete: false`. Его исторический источник `audit/reports/G2-JIRA-MEMBER-JOINS.md:301` учитывает MOS-1419 как **U / UN**, `I(47)/subtasks/3 → S(5)`. Отдельного overlay MOS-1419 в текущем coverage нет. Это состояние аналитического join, не доказательство отсутствия реализации.

## 4. Код и тесты: observed

| Доказательство | Наблюдение |
|---|---|
| `app/pages/dialogs/ui/dialog-table/dialog-table-row.tsx:57–59` | Ячейка без преобразования передаёт `row.operator_rating` в `DialogOperatorRating`. |
| `app/entities/dialog/ui/dialog-operator-rating.tsx:7–8` | При `null` компонент явно возвращает видимый текст «Нет оценки». Причина дефекта локализована. |
| `app/entities/dialog/ui/dialog-operator-rating.test.tsx:19–24` | Тест `null` требует «Нет оценки» и отсутствие звёзд. Он закрепляет неверный текст, а не R1. |
| `app/pages/dialogs/ui/dialogs-page.test.tsx:143–171` | Компонентный сценарий строки также ожидает «Нет оценки» — строка 162. |
| `app/entities/dialog/ui/dialog-operator-rating.test.tsx:6–18` | Есть проверки оценок 1–5, количества звёзд и доступного имени. Это существующая защита соседнего поведения, не новое покрытие R1. |

Компонент имеет другие потребители: `app/pages/dialog-details/ui/dialog-details/dialog-summary.tsx:50–56` и `dialog-operators.tsx:72`. Поэтому глобальная замена его null-представления может затронуть карточку, которая не входит в эту подзадачу.

Тесты только прочитаны; их прохождение не утверждается.

## 5. Findings и минимальная плановая коррекция

### F1. Несоответствие реализации R1

**Expected:** прочерк при `operator_rating: null` в реестре.  
**Observed:** «Нет оценки» в компоненте и двух тестовых ожиданиях.  
**Unknown:** воспроизводимость на развёрнутом окружении и состояние исправления вне данного HEAD.

### F2. Недостаточная точность спецификации

OpenSpec допускает текущее обобщённое представление «отсутствие оценки» и не обеспечивает точную проверку MOS-1419.

### Рекомендация: NEW corrective change; KEEP исторические артефакты

Предложить родителю новый узкий change, например:

- `openspec/changes/fix-dialog-registry-unrated-placeholder/proposal.md`;
- `openspec/changes/fix-dialog-registry-unrated-placeholder/tasks.md`;
- `openspec/changes/fix-dialog-registry-unrated-placeholder/specs/dialog-registry/spec.md`.

Это предлагаемые, **не созданные** артефакты.

Минимальное содержание:

1. В delta `MODIFIED Requirements` сохранить полный блок `Registry represents server rows faithfully`, добавив: при `operator_rating = null` ячейка оценки реестра показывает прочерк, не видимый текст «Нет оценки», независимо от завершённости.
2. Добавить самостоятельный сценарий отсутствующей оценки для завершённого и незавершённого диалога; сохранить соседние требования блока.
3. Открытой задачей запланировать исправление ячейки `dialog-table-row.tsx`, не меняя без необходимости null-представление карточки.
4. Открытой задачей запланировать обновление ожидания в `dialogs-page.test.tsx` и адресные проверки ячейки: `null` при обоих состояниях завершения; отсутствие звёзд и видимого «Нет оценки»; сохранение числовой оценки 1–5.
5. Если меняется общий `DialogOperatorRating`, отдельно проверить его потребителей и обновить `dialog-operator-rating.test.tsx` согласно выбранному контекстному API, без расширения R1 на карточку.

API/schema edits не нужны. Продуктовый вопрос о самом прочерке не блокирует планирование: требование явно сохранено. Конкретный Unicode-символ прочерка источники не фиксируют.

Исторические ledger, архивные specs и feature-checkboxes сохраняются. После независимого ревью допустим отдельный additive overlay аналитического покрытия; не объявлять исправление доставленным.

## 6. SHA256 входов

Хеши вычислены по байтам локальных файлов.

| Файл | SHA256 |
|---|---|
| `audit/work-items/WAVE-D090-EIGHT.md` | `98e63a056d15acd94e6bcf2fa78065bc5ea4ebf9ddc2bcf13cfaf2b3900f871b` |
| `audit/coverage.json` | `e93adb588725fb39b55f278270ad33e4d7e9da8ac73ee4620d4c0293740d791b` |
| `audit/sources/jira-subtasks/r1/content.json` | `c4c86b024d8e0ef30bd5234eb13ee2a9a85d4fa29eeb9cb2a37c024d75d3652e` |
| `audit/sources/jira-subtasks/r1/metadata.json` | `d9c0f1c289e6f2d675b5cc07994956fa039e846919b08726d637f027279cfe20` |
| `audit/sources/wiki-241085439/r1/content.json` | `974ea35aaf44b9ec7c14c573ba58bdf7ed55397a9ca47d62b37fb39d9886f8bc` |
| `audit/sources/wiki-241085439/r1/metadata.json` | `dcaab775172b7e615dfae64184d719f8403cff1fb304650ba21e1532ce577b7d` |
| `audit/sources/wiki-243776365/r1/content.json` | `2f659b5423fa7203dcd4f70743e59aabfb571452144394621091ff2cd58cab55` |
| `audit/sources/api-live/r2/content.json` | `ab5527772e16273222bad8a5f4a35ffe1de4e612630e1111e2f5612db4996993` |
| `openspec/specs/dialog-registry/spec.md` | `ef9e52b7dba2ff4f0fa1dd1a9fa3d7cfaa78890277c376d70ed0301423bf6f83` |
| `app/entities/dialog/ui/dialog-operator-rating.tsx` | `089bf7705ca41e9117cffea1c219fb3c6171169608761ba8f01415845395ad04` |
| `app/entities/dialog/ui/dialog-operator-rating.test.tsx` | `c89d3b406354b00dee2ee0863ddf3a761e25c495a8e2ce9e6c2a45c5b6a9de0d` |
| `app/pages/dialogs/ui/dialog-table/dialog-table-row.tsx` | `3096df76cead86dad46f13be6cbde70de0a2c0d009c0842f82087f89ad985de3` |
| `app/pages/dialogs/ui/dialogs-page.test.tsx` | `3dba3eb88505d29a2ed80dab6c301e0496007e85a26749d74b80a747824d2fec` |

Хеши Jira content и wiki content совпадают с соответствующими сохранёнными metadata.

## 7. Ограничения

- Jira attachment `$.items[5].attachments[0]`, ID `839862`, сохранён только как metadata; изображение не исследовано.
- Comments/custom acceptance fields отсутствуют в извлечении.
- Несуществующий readable-каталог wiki не использовался как источник: прочитан доступный исходный JSON `$.bodyView`.
- Проверки выполнены статически; тесты, build, lint, typecheck и browser/E2E не запускались по контракту.
- Нет выводов о deployment, полном покрытии MOS-1037 либо завершении всей волны.