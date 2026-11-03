# JOIN-MOS-1166 — длинное описание навыка на шаге «Сценарии»

## Граница проверки

Статическая предметная сверка только MOS-1166. HEAD по контракту волны: `bc0d9800f25a90989b9c73c76f91996f8300f1d3` (повторно через git не проверялся). Сеть, браузер, тесты и business API не запускались. Изменён только этот отчёт; исторические ledgers, checkbox и архивы сохранены. Deployment и закрытие Jira не подтверждаются.

Ниже `audit/` означает `openspec/changes/reconcile-control-center-backlog/audit/`; JSON-индексы начинаются с нуля.

## Точный источник и атомарные требования

Прочитано **тело**, а не только summary: `audit/sources/jira-subtasks/r1/content.json#/items/13`, строки 267–284: key MOS-1166, parent MOS-709, status Backlog, updated `2026-10-09T15:07:28.233+0800`. Подтверждение членства: `audit/sources/jira-member-index/r1/content.json#/items/118/subtasks/3`, строки 1027–1031.

| Атом | Локатор | Expected |
|---|---|---|
| Условие | `/items/13/description`, «Предусловие» | В реестре есть навык с длинным описанием около 200 символов. Это пример для воспроизведения, не лимит данных. |
| Место | Там же, шаг 1 | Добавление поверхности → «Сценарии». Не реестр навыков и не произвольная карточка. |
| R1 | Там же, «ОР: Длинное описание навыка обрезается» | Визуальное обрезание длинного текста. Число строк, ellipsis и tooltip источником не определены. |
| R2 | Там же, «ФР: … появляется горизонтальный скролл» | Устранение горизонтальной прокрутки, вызванной длинным описанием. Это вывод из прямо описанного негативного результата, а не отдельное требование API. |

Тело присутствует — gap отсутствующего requirement body нет. `/items/13/attachments/0` перечисляет `832305`, `3.png`, image/png, 120531 байт; тело изображения не сохранено согласно `jira-subtasks/r1/metadata.json#/limitations`. Поэтому точный прежний элемент и геометрия screenshot неизвестны. Комментарии/custom acceptance fields также не собраны. Указанный в description адрес контура не открывался.

Повторно использованы только границы исторического inventory `audit/reports/JIRA-MOS-783.md:52–68` и member join `audit/reports/G2-JIRA-MEMBER-JOINS.md:309` (MOS-1166 = U/UN). `audit/coverage.json:1–6,118–126` сохраняет partial, complete=false и acceptedEvidenceThrough=D-089; отдельного принятого overlay MOS-1166 нет. Эти записи не доказывают исправление и не заменяют приведённую выше сверку тела. Wiki `audit/sources/wiki-241080065-readable/r1/content.txt:17–23` подтверждает шаг выбора сценариев, но не задаёт обрезание текста.

## Owner: main / delta / archive

- Непосредственный owner общего элемента выбора: `openspec/specs/surface-skill-selection/spec.md`, requirements **Contract-backed skill catalog**, **Domain and bulk selection**, **Registration and existing surface persistence**. Они определяют каталог, доступный выбор и запись, но не требуют визуального обрезания описаний.
- Контекст мастера: `openspec/specs/surface-registration/spec.md`, **Creation supports an atomic optional configuration**, **Empty production catalog explains registration blocking and recovery**. Последнее относится к пустому каталогу, не к длинному тексту.
- Архивный owner каталога: `openspec/changes/archive/2026-10-02-mos-911-prod-skill-selection/specs/surface-skill-selection/spec.md`, одноимённые требования каталога и массового выбора. Требования обрезания там нет; архив не менять.
- По локальному поиску owner-файлов и текста specs отдельная активная delta MOS-1166/обрезания описания на этом шаге не найдена. Общее покрытие MOS-911 нельзя засчитать за исполнение MOS-1166.

## API и важное различие полей

Сохранённый `audit/sources/api-live/r2/content.json`:

- `/paths/~1api~1control~1api~1skills~1v1~1skills/get` — каталог навыков;
- `/components/schemas/SkillListItemResponse/properties/purpose` — string без maxLength; **description в свойствах этой list-схемы отсутствует**;
- `/components/schemas/tsam__assistant_management__skills__endpoints__http__schemas__SkillResponse/properties/description` — string либо null; соседний `/properties/purpose` — отдельное поле.

Текущий `app/entities/skill/api/skill-registry-client.ts:23–42,54–88` принимает `purpose: z.string()`, возвращает items без сокращения и собирает страницы. Текущий UI выводит именно `skill.purpose`, не detail.description. Поэтому нельзя без доказательства отождествить слово «описание» в старой Jira с конкретным API-полем `description` или объявить ошибкой отсутствие дополнительного detail-запроса. Список сейчас предоставляет текст назначения.

Визуальное ограничение строки не требует нового endpoint, payload или maxLength=200. Полный текст должен оставаться данными; обрезание значения при чтении/отправке не является исправлением этой UI-задачи. Снимок API не подтверждает фактическую работу backend или развертывание.

## Observed: код и тесты

| Доказательство | Наблюдение и граница вывода |
|---|---|
| `app/widgets/surface-registration/ui/surface-registration.tsx:16,68–73`; `app/features/surface-registration/ui/surface-registration-step-content.tsx:23–33` | Реальный шаг «Сценарии» получает общий SurfaceSkillSelectionEditor. Это прямая цепочка до текущего элемента, не вывод по названию модуля. |
| `app/features/surface-skill-selection/ui/surface-skill-selection-editor.tsx:20–24,58–62`; `.../surface-skill-selection-editor/catalog-section.tsx:44–55` | Продовый каталог группируется и передаётся в группы; Card имеет `overflow-hidden`. Это защитный признак контейнера, но не доказательство обрезания конкретного текста или отсутствия скролла страницы. |
| `app/features/surface-skill-selection/ui/surface-skill-selection-editor/skill-selection-item.tsx:14–34` | Grid использует `sm:grid-cols-[minmax(0,1fr)_minmax(280px,1fr)]`. Абзац purpose имеет только `text-sm text-muted-foreground sm:text-right`: нет локального truncate/line-clamp/overflow ограничения. `min-w-0` на строках 25–27 относится к имени, не абзацу purpose. |
| Тот же файл `:18,29–34` | `aria-describedby` связывает переключатель с полным purpose. При будущем визуальном исправлении эту доступность нельзя потерять. |
| `app/features/surface-skill-selection/ui/surface-skill-selection-editor.test.tsx`, describe SurfaceSkillSelectionEditor и helper skill в конце файла | Прочитанные тесты проверяют клавиатуру, mixed state, параметры, prod-фильтр и ошибки. Fixture purpose — короткое «Назначение». Отдельного случая примерно 200 символов, неразрывной строки или утверждения обрезания нет. |

**Observed:** отсутствует явное ограничение длинного текста именно в абзаце; существующий контейнер скрывает overflow. Это статический риск и пробел regression evidence, **не доказанный текущий горизонтальный скролл**. Текст с пробелами может переноситься; реальная геометрия зависит от ширины и содержимого.

**Unknown:** исходный текст из screenshot, соответствие старого «описания» текущему purpose/detail.description, желаемая кратность строк, поведение на фактических ширинах, deployment. Не превращать эти неизвестные в утверждение о воспроизведённом дефекте.

## Минимальные решения

1. **Keep:** существующий API-каталог, prod-фильтрацию, полный purpose, accessible description, параметры и выбор. Не добавлять detail-fetch и ограничение длины данных ради UI.
2. **New (планирование, после независимого review):** узкая delta, например `openspec/changes/fix-surface-skill-description-overflow/{proposal.md,tasks.md,specs/surface-skill-selection/spec.md}`. Одно ADDED requirement: отображаемый описательный текст навыка на шаге регистрации визуально ограничен и не вызывает горизонтального переполнения, без изменения полного значения и доступного описания. Это кандидат, файлов сейчас не создано. Включение в общий surface corrective change допустимо без дублирования owner.
3. **Update (будущая реализация, не выполнено):** точечный layout в `app/features/surface-skill-selection/ui/surface-skill-selection-editor/skill-selection-item.tsx`; тест в `app/features/surface-skill-selection/ui/surface-skill-selection-editor.test.tsx` для обычного короткого purpose и около 200 символов, включая неразрывный текст, сохранности значения/aria-describedby и выбора. Component assertions на классы/DOM не выдавать за измерение browser geometry. Общий компонент используется также редактированием поверхности: учитывать регрессию, но не расширять исходное требование на весь модуль.
4. **Question:** перед изменением семантики выводимого поля уточнить, имеется ли в виду текущий purpose или именно detail.description; для чистого визуального ограничения текущего текста это не повод менять API. Способ сокращения уточнять только в необходимом объёме: источник не требует конкретного tooltip или числа строк.

Итог: частичный предметный join с явным specification/test gap, не закрытие MOS-1166. Новых политик, запуска тестов или изменения исторических статусов не предлагается в рамках этого отчёта.

## SHA256 ключевых входов

Хеши пересчитаны локально по байтам, не перенесены только из metadata.

| Путь | SHA256 |
|---|---|
| `audit/work-items/WAVE-D090-EIGHT.md` | `98e63a056d15acd94e6bcf2fa78065bc5ea4ebf9ddc2bcf13cfaf2b3900f871b` |
| `audit/work-items/WAVE-D090-REVIEW-NEXT.md` | `fdf9ed7a57cc427bf9feb58639fe976fb2f76fb1bd9082c0f1626649cfdfcc72` |
| `audit/sources/jira-subtasks/r1/content.json` | `c4c86b024d8e0ef30bd5234eb13ee2a9a85d4fa29eeb9cb2a37c024d75d3652e` |
| `audit/sources/jira-subtasks/r1/metadata.json` | `d9c0f1c289e6f2d675b5cc07994956fa039e846919b08726d637f027279cfe20` |
| `audit/sources/jira-member-index/r1/content.json` | `dba6cffa66e0aef23e9ef34c4a52215a5c02d31e7da1dca87888e821198b8043` |
| `audit/sources/api-live/r2/content.json` | `ab5527772e16273222bad8a5f4a35ffe1de4e612630e1111e2f5612db4996993` |
| `audit/coverage.json` | `e93adb588725fb39b55f278270ad33e4d7e9da8ac73ee4620d4c0293740d791b` |
| `audit/reports/JIRA-MOS-783.md` | `4088bb978c718cee5104e570f42ab0b99191a4035f5f9752a80e098153b56354` |
| `audit/reports/G2-JIRA-MEMBER-JOINS.md` | `dc9b199c2a9500b2ff1857de1feaec9282e8130fa1b78720f551913907618b44` |
| `openspec/specs/surface-skill-selection/spec.md` | `e27eb8b354e4370da3519b5387cff5369a2f083e6c3be05f82d8631746c19ee0` |
| `openspec/specs/surface-registration/spec.md` | `31928d907bfff75eca61d2efe176879e3c7f4d3e0029dbe6bb97258b8d00f9a5` |
| `openspec/changes/archive/2026-10-02-mos-911-prod-skill-selection/specs/surface-skill-selection/spec.md` | `17ddca2bdb446f562c47bbe0af30807829a140addce6ff68241f547ae230e44a` |
| `app/features/surface-skill-selection/ui/surface-skill-selection-editor/skill-selection-item.tsx` | `8651038c1d4bc340d8763db4ed45b607c27dcddaa6371a7a1c43187eaa7496af` |
| `app/features/surface-skill-selection/ui/surface-skill-selection-editor.tsx` | `fd89c9208b2c8f6e144849c6dccd3541ea36d282ce9364f8563c0168365df6be` |
| `app/features/surface-skill-selection/ui/surface-skill-selection-editor.test.tsx` | `223c5241a669d93aebdcc756b902e67b6969a24fa275eec0ca9b1645d3af7c9e` |
| `app/entities/skill/api/skill-registry-client.ts` | `fe22d8076a52c22ea245853b2bbe3f7103a1f515776920a6ecf76b6a6fcd5969` |
| `app/widgets/surface-registration/ui/surface-registration.tsx` | `30211e1b4a5534bb0292292fe0560045bb1cdf34e7f642daae4184754b7d089c` |

```acceptance-report
{
  "criteriaSatisfied": [{"id":"criterion-1","status":"satisfied","evidence":"Прочитано /items/13/description MOS-1166; сопоставлены owner, API, конкретный UI и component-тесты; unknown отделены от наблюдений."}],
  "changedFiles": ["openspec/changes/reconcile-control-center-backlog/audit/reports/JOIN-MOS-1166.md"],
  "testsAddedOrUpdated": [],
  "commandsRun": [{"command":"python: локальное чтение JSON и вычисление SHA256","result":"passed","summary":"Найден точный элемент MOS-1166, проверены схемы и хеши ключевых входов."},{"command":"тесты / browser / network","result":"not-run","summary":"Запрещены заданием."}],
  "validationOutput": ["Тело требования найдено; обрезание текущего текста не имеет отдельного spec/test доказательства."],
  "residualRisks": ["Screenshot не сохранён; purpose и description нельзя автоматически отождествлять.","Геометрия и deployment не проверялись."],
  "noStagedFiles": true,
  "diffSummary": "Создан только назначенный аналитический отчёт; проект и исторические реестры не менялись.",
  "reviewFindings": ["Требуется независимое review; текущий горизонтальный скролл не доказан статикой."],
  "manualNotes": "Тесты прочитаны, но не запускались. Git mutations не выполнялись; noStagedFiles означает отсутствие staging действий агента, состояние индекса не проверялось."
}
```
