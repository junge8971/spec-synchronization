# JOIN-MOS-674 — точное сопоставление исторического требования с текущими владельцами

## Результат и граница

Выполнен только JOIN-MOS-674: сохранённое тело MOS-674 сопоставлено с текущим механизмом хлебных крошек и существующими проверками. **Механизм статически обнаружен; оснований создавать повторную задачу реализации или менять CLOSED не установлено.**

Новый результат — отдельный member join для MOS-674, ранее представленного историческим основанием `REQ-MOS-905-018`. Это не повторная проверка всех 18 требований MOS-905 и не новая приёмка реализации.

Файлы не изменялись. Публикация не выполнялась. Отчёт предназначен для сохранения runtime в `openspec/changes/reconcile-control-center-backlog/audit/reports/JOIN-MOS-674.md`.

## 1. Источник и принятая карта

Здесь `A` = `openspec/changes/reconcile-control-center-backlog/audit`, `C` = `A/sources/jira-shell-details/r1/content.json`.

Точные указатели:

- `C /items/3/key`: `MOS-674`.
- `/items/3/summary`: `[FE] Создания механизма хлебных крошер`.
- `/items/3/description`: «Создать хлебных крошек и сделать так чтобы они автоматически отображались на каждой странице».
- `/items/3/status`: `CLOSED`; `/items/3/parent`: `null`. Прямую родительскую связь по этому полю установить нельзя.
- `/items/3/retrievedAt`: **2026-10-16T12:45:22.008Z**; общий cutoff пакета `/retrievedAt`: **2026-10-16T12:45:22.199Z**.
- `/items/3/comments/items/0`: ID `1114562`, историческое сообщение об успешном тестировании на `https://mobile-a-tech.mos.ru/tsam-panel`, создано `2026-09-22T21:44:47.947+0800`.
- `/items/3/comments`: сохранены 1 из 1 комментариев при `startAt=0`; это согласовано с `metadata.json /comments/3`, но ничего не говорит о последующих изменениях Jira.
- `/items/3/attachments/0–2`: только метаданные изображений `817144`, `825968` и HTML-прототипа `817143`; тела не собраны.

Прочитаны прежние `reports/REQ-MOS-905.md`, `reports/IMPL-MOS-905.md`, `reviews/RECON-MOS-905.md`, `reviews/R-IMPL-MOS-905.md` как карты обнаружения. Принятое ограничение проверено в `A/decisions.md:629–643`, D-009/D-008: mapping принят с поправками, исторические отчёты сохраняются; нельзя превращать уточнения действующих правил в новые задачи или runtime-приёмку.

## 2. Точные member joins: expected / observed / unknown

| Join | Expected | Observed — текущие файлы | Unknown / предел |
|---|---|---|---|
| **674-A: автоматическое подключение** | MOS-674 `/description`: общий механизм, автоматически отображаемый на страницах. | `app/application/ui/application-layout.tsx:6,17–41`: общий layout импортирует публичный API breadcrumbs и монтирует один `ApplicationBreadcrumbs`, передавая маршруты. `app/widgets/breadcrumbs/index.ts:1` экспортирует компонент. `app/widgets/breadcrumbs/ui/application-breadcrumbs.tsx:18–39` определяет текущий маршрут через `useLocation`/`matchRoutes`, без ручного добавления крошек в каждую страницу. | Это статическая композиция, не проверка каждой страницы в запущенном приложении. Layout явно ограничивает показ `access.allowed`; политика доступа здесь не переаудировалась. |
| **674-B: владелец структуры** | Историческое тело не задаёт точные подписи или иерархию. Современное уточнение: `openspec/specs/control-center-shell/spec.md:260–282`. | `app/shared/config/constants/application-routes.constants.ts:17–142` хранит `breadcrumb`, `parentPath`, `tabs`. `app/application/constants/application-routes.constants.ts:1–6` составляет общий реестр; `app/routes.ts:6–14` использует его для регистрации маршрутов. Компонент крошек использует переданный реестр и родительский путь (`application-breadcrumbs.tsx:23–39`). | Наличие optional-экспортов в составе реестра не доказывает корректность каждого optional-маршрута; их внутренности не проверялись. |
| **674-C: предел «каждой страницы»** | Текущий shell-spec `:262` прямо запрещает крошки на `/` до redirect и элемент «Главная». Это уточнение исторической общей формулировки, не новый дефект MOS-674. | `application-breadcrumbs.tsx:25` возвращает `null` для неизвестного маршрута и `/`. `application-breadcrumbs.test.tsx:72–87` содержит отдельные проверки `/` и `/missing`: нет breadcrumb navigation и separator. | Не заявляется универсальное отображение в состояниях ошибки, отказа доступа или до готовности оболочки. Историческое CLOSED не доказывает такую универсальность. |
| **674-D: ссылки и текущий элемент** | Shell-spec `:262,274–277`: ссылка на реестр, подпись вложенного экрана, канонические адреса под basename, доступное обозначение текущего элемента. | `application-breadcrumbs/breadcrumb-trail.tsx:15–32`: `nav`-представление с именем «Хлебные крошки», React Router `Link`, `BreadcrumbPage`. `application-breadcrumbs.test.tsx:15–37` независимо задаёт два случая `/skills/new` и `/surfaces/new`, проверяет родительские ссылки под `/tsam-panel`, два элемента, `aria-current="page"`, отсутствие «Главная» и отсутствие detail-fetch. | Это прочитанные assertions, не результат запуска. Визуальное соответствие историческим изображениям неизвестно. Полный аудит accessibility примитива не проводился. |
| **674-E: вкладки и динамические подписи — современные владельцы, не новые требования MOS-674** | Shell-spec `:260–282` уточняет вкладки, динамические карточки и fallback. Сам MOS-674 не содержит этих правил. | `application-breadcrumbs.tsx:42–53` выбирает вкладку и делегирует карточки. Дочерние файлы: `skill-details-breadcrumbs.tsx:8–19` — имя/«Навык»; `surface-details-breadcrumbs.tsx:8–22` — имя/«Поверхность»; `dialog-details-breadcrumbs.tsx:8–14` — topic/`Диалог <chat_id>` либо нейтральный «Диалог». Все используют публичные API entities. Тест `application-breadcrumbs.test.tsx:39–71` проверяет вкладки, `:89–111` — имя навыка, `:150–175` — имя поверхности. | Матрица вкладок получает ожидаемые значения из того же реестра: это не независимое доказательство правильности всех подписей. Диалоговые сценарии других тестовых файлов в этом join заново не проверялись. Бизнес-карточки не входят в приёмку MOS-674. |

**Текущая граница владения:** композиция — `app/application`; метаданные — `app/shared/config`; построение и отображение — слайс `app/widgets/breadcrumbs`; данные карточек — публичные API соответствующих entities. Шапка MOS-672, меню MOS-673, redirect/history и остальные требования MOS-905 этому member не присваиваются.

## 3. Минимальная классификация

- **keep:** сохранить историческое требование и CLOSED MOS-674 как данные снимка. Общий механизм существует в текущем коде; повторное «создать хлебные крошки» не обосновано.
- **update — только кандидат для родительской очереди:** дополнить доказательную карточку MOS-674 точным join с владельцами и оговоркой: современный shell-spec уточняет историческое «каждой страницы», включая отсутствие крошек на корне. Сохранить связь с `REQ-MOS-905-018`, не создавать второе независимое требование на ту же реализацию.
- **new:** нет обоснованной новой продуктовой или implementation-задачи.
- **question:** обязательного решения для этого join нет. Вопрос визуальной эквивалентности остаётся непроверенным из-за отсутствия attachment bodies, но не блокирует сопоставление доступного текстового требования.

Предлагаемый текст **для добавления родителем в `pending-publication.md`, не для непосредственной публикации**:

> MOS-674: историческое требование автоматических хлебных крошек сопоставлено с общим ApplicationLayout, реестром маршрутов и ApplicationBreadcrumbs. Современные исключения и иерархия определены control-center-shell/spec.md:260–282; это уточнение исторической формулировки, а не основание повторно создавать механизм. Код и существующие assertions прочитаны; тесты не запускались. CLOSED и комментарий 1114562 относятся к сохранённой истории, не подтверждают текущий deployment. Статус и продуктовые требования не менять на основании этого join.

## 4. Хеши входов

SHA-256 вычислены заново по полным байтам файлов read-only-командой Python. Для `C` подтверждены **14311 байт** и совпадение с `metadata.json /sha256`.

| Вход | SHA-256 |
|---|---|
| `A/work-items/WAVE-D093-LOCAL-EIGHT.md` | `bfed26db7f9865a85e19e0cdfbeb0b92fc7b2b16999be3dac4d1cb92bd5eaf4e` |
| `C` | `30caeb33afa1ae7f9be6c55b9157687174e3bd786dd73a54693e78979b4deef4` |
| `A/sources/jira-shell-details/r1/metadata.json` | `ae842c6c481369e871263f49ad0c58fc9b078ea760c9bb37c20aa400a8854dcb` |
| `A/reports/REQ-MOS-905.md` | `9ed8abd75e53e4667d8123e63721470238d0adb9eb6655f7101105ed2b2127d6` |
| `A/reports/IMPL-MOS-905.md` | `392d18a12350147f7023bf87eeca8d3c244bb29e3592e7d744061a196ba5fdef` |
| `A/reviews/RECON-MOS-905.md` | `a11af36d27809059d318d2611e92678ad56e132fbe877c6a89c92e88f29d9458` |
| `A/reviews/R-IMPL-MOS-905.md` | `c6702fe75bf0802cc7b181093c7664bb6b00f6878d7ffcc267fae32d082d312e` |
| `A/decisions.md` | `6cce36bc512cc01cd7ef1552fa29676fd385243a37e14720352a0de27564632f` |
| `openspec/specs/control-center-shell/spec.md` | `4274bde7ecdf7e18bdcf73cb1755886f3e61bc2cbea3728da0a382006dd0276f` |
| `app/routes.ts` | `3b7d7a026d0f73baa121d33407f155cadf9a18ffe5f0a618ad74bc02481594c4` |
| `app/application/constants/application-routes.constants.ts` | `53bc9d61287ea25e292f5410f1905d1718adbefe3f44d6422a6447a183b3230c` |
| `app/application/ui/application-layout.tsx` | `5d4ec467833bece6f0a5f3c96fe61b0355ace670bc8525f726c6b5e6fc021b30` |
| `app/shared/config/constants/application-routes.constants.ts` | `bf50517737722446a5999e1c09ba3b2c603cc837cee23a8ab871e6418c29a21d` |
| `app/widgets/breadcrumbs/index.ts` | `6e51e2f7ff8609fc02dc4f2d7694c4186c1ccbc86c499718814a56e4e5b2b051` |
| `app/widgets/breadcrumbs/ui/application-breadcrumbs.tsx` | `6a7715fd81ad7c7b9c591dc784b33ea55e677899139beda3bb967f75bd7ecac9` |
| `app/widgets/breadcrumbs/ui/application-breadcrumbs.test.tsx` | `5edbe5242cf6c32d7cafc6b81026fc299ad13297655a568c3c65bd69227164e6` |
| `app/widgets/breadcrumbs/ui/application-breadcrumbs/breadcrumb-trail.tsx` | `1f321b0009c6f99c525b829982b912be6fd078f1b16696446aa7697eab2d60fc` |
| В том же каталоге `dialog-details-breadcrumbs.tsx` | `1e5d292f38efe850637cdf8ae02f22093f831ab43488f87299409a7d16e83861` |
| В том же каталоге `skill-details-breadcrumbs.tsx` | `7d51fb6975e8b9ea9e6bdde5c6b21ad23192595a5e75238ef133b088dc7ab463` |
| В том же каталоге `surface-details-breadcrumbs.tsx` | `1647e98e85526dd44bd7d9cdfc54eb02cfbf20b3da11d0f766403df04af9bc90` |

## 5. Ограничения

- Исторический источник ограничен cutoff 16 октября 2026 года; текущие Jira, комментарии и статус не запрашивались.
- Тела вложений и custom fields отсутствуют в пакете. Это препятствует визуальному сравнению, но не текстовому join.
- Комментарий об успешном тестировании — историческое утверждение автора, не проверка текущего checkout или deployment.
- Тесты, сборка, сеть и браузер не запускались. Assertions прочитаны; успешное выполнение не заявляется.
- Git не использовался; baseline из задания не подтверждался, индекс не проверялся. Хеши фиксируют прочитанные файлы, а не идентичность checkout заданному commit.
- Обязательные локальные входы для ограниченного join доступны; blocker отсутствует.