# JOIN-MOS-673 — точное сопоставление исторической навигации

## Результат и границы

**MOS-673 сопоставлен с текущим владельцем навигации; планировочный результат — keep, без нового продуктового change.** Получено новое member-specific evidence, а не повторная приёмка MOS-904/905.

Обязательное сохранённое тело доступно. Блокера для ограниченного сопоставления нет. **Соответствие историческому наполнению примера/скриншота неизвестно:** пакет содержит только метаданные вложений.

Отчёт предназначен для `audit/reports/JOIN-MOS-673.md`. Файлы инструментами не записывались. Публикация, изменение реестров покрытия и `pending-publication.md` остаются исключительно за parent после review.

Здесь и далее:

- `A` = `openspec/changes/reconcile-control-center-backlog/audit`;
- `J` = `A/sources/jira-shell-details/r1/content.json`;
- `S` = `openspec/specs/control-center-shell/spec.md`.

## 1. Точный источник и исторический предел

Проверен именно **`J#/items/2/key = MOS-673`**:

| Локатор | Сохранённые сведения |
|---|---|
| `/items/2/summary` | `[FE] Создание навигации админки` |
| `/items/2/description` | «Сделать навигацию аналогичную по наполнению согласно примеру и скриншоту», ссылка на `image-2026-09-03-13-29-40-640.png` |
| `/items/2/status` | `CLOSED` — исторический workflow status |
| `/items/2/updated` | `2026-09-23T17:21:47.836+0800` |
| `/items/2/retrievedAt` | `2026-10-16T12:45:21.808Z` |
| `/items/2/comments/items/0` | ID `1115041`, сообщение об успешном тестировании на `https://mobile-a-tech.mos.ru/tsam-panel`, дата `2026-09-23T17:21:09.555+0800` |
| `/items/2/attachments/0` | ID `817141`, исходный PNG, 24010 bytes |
| `/items/2/attachments/1` | ID `826497`, PNG результата, 31195 bytes |
| `/items/2/attachments/2` | ID `817140`, `Прототип ЦАМ, версия MVP.html`, 1158654 bytes |

Пакет получен **2026-10-16T12:45:22.199Z**. Проверены 14311 bytes и совпадение SHA256 с `metadata.json#/sha256`; сохранён один комментарий при `total=1`, три записи метаданных вложений. Это полнота сохранённой выборки, не текущего Jira.

`metadata.json#/membership` относит member к MOS-624; сам `J#/items/2/parent` равен `null`. Прямая parent-связь из detail-body не доказана. Метаданные коллектора не являются независимой проверкой remote authenticity.

**Из тела MOS-673 нельзя восстановить названия, порядок и количество исходных пунктов меню.** Современное меню ниже не выдаётся за содержимое отсутствующего прототипа. CLOSED и комментарий о тестировании не подтверждают нынешний checkout или deployment.

## 2. Использование предыдущих результатов

Карты discovery: `A/reports/REQ-MOS-904.md`, `REQ-MOS-905.md`, `IMPL-MOS-904.md`, `IMPL-MOS-905.md`; проверены implementation reviews и релевантные reconciliation corrections.

Принятие и ограничения подтверждены `A/decisions.md:623–643`, D-008/D-009/D-010:

- существующие shell requirements уже владеют современными группами, маршрутами, документацией и мобильной навигацией;
- нельзя превращать неполное Jira wording в новый продуктовый пробел;
- отдельные component tests не доказывают production-root/deployment;
- исправления review MOS-905 сохраняются; fallback-политика не переоткрывается.

`A/reports/G2-JIRA-MEMBER-JOINS.md:141` исторически содержит `MOS-673 | U | UD: SH(2) source detail, not SH output token`. Настоящий отчёт добавляет **явное сопоставление `/items/2/description` → текущий owner → прочитанные implementation/assertions**, которого не заменяет принятие соседнего MOS-904.

## 3. Новое точное member-сопоставление

### JOIN-MOS-673-01 — наполнение навигации

**Expected из MOS-673:** навигация аналогична по наполнению историческому примеру и скриншоту. Других перечисленных критериев в сохранённом description нет.

**Observed сейчас:**

- `app/shared/config/constants/application-routes.constants.ts:23–140` задаёт базовые пункты:
  - основная группа: Навыки `/skills`, Поверхности `/surfaces`, Песочница `/sandbox`;
  - Аналитика: Диалоги `/dialogs`, Дашборд `/metrics`, Отчёты `/reports`;
  - Эксплуатация: Состояние системы `/ops`, Команды `/teams`;
  - footer: Документация `/docs`.
- `app/shared/config/application-routes.ts:19–52,56–69` строит группы и footer из route descriptors.
- `app/widgets/navigation/ui/application-navigation.tsx:27–72` действительно отображает группы и footer, а не отдельный неиспользуемый список.
- `app/shared/config/application-routes.test.ts:15–27,37–65` содержит assertions для девяти **базовых** пунктов, трёх групп, точных labels/hrefs и отсутствия отдельных пунктов `/new`/динамических карточек.
- `app/widgets/navigation/ui/application-navigation.test.tsx:12–34` содержит assertions для labels/hrefs, групп и отсутствия подписи «Подключение».

**Современный нормативный owner:** `S:48–89`, requirement `Navigation consumes confirmed access and route availability`. Это согласованный современный контракт, **не расшифровка отсутствующего изображения MOS-673**.

**Unknown:** историческое совпадение списка, порядка, иконок и визуального наполнения. Девять пунктов — не утверждение о полном production-меню: `app/application/constants/application-routes.constants.ts:1–6` добавляет optional routes, а `app/application/ui/application-layout.tsx:19–34` передаёт сформированные и отфильтрованные группы. Optional-модули и permission policy в этой lane не аудитировались.

**Вывод:** keep существующего owner; отсутствие historical parity evidence не доказывает дефект.

### JOIN-MOS-673-02 — рабочая современная навигация и выделение

**Expected:** навигационный механизм относится к member MOS-673; конкретные современные правила активного раздела заданы отдельно в `S:28–41,83–85`, а не перечислены в historical body.

**Observed:**

- `app/routes.ts:6–14` регистрирует route descriptors.
- `app/widgets/navigation/ui/application-navigation/navigation-entry.tsx:36–46` использует React Router `Link`, `item.href`, `isActive` и callback перехода.
- `app/shared/config/application-routes.ts:71–79` сопоставляет точный адрес либо вложенный путь с границей `/`.
- `application-navigation.tsx:28–30,49–52` вычисляет активный пункт по переданным группам.
- `application-navigation.test.tsx:36–54` явно проверяет parent highlight для `/ops`, `/teams`, `/skills/new`, `/surfaces/new`, `/surfaces/example`, `/dialogs/example`.
- `app/shared/config/application-routes.test.ts:15–27` дополнительно проверяет отсутствие дублей меню для вложенных экранов.
- `app/widgets/navigation/model/get-navigation-item-state.ts:5–14` и `navigation-entry.tsx:13–33` реализуют disabled-представление для `routeAvailable === false`, с пояснением вместо рабочей ссылки.

**Unknown:** выполнение этих assertions и реальные переходы в deployment. Наличие route/link не подтверждает готовность бизнес-функций назначения.

**Вывод:** keep. Это точное evidence современного продолжения навигации MOS-673, без присвоения ей всей маршрутизации MOS-905 или breadcrumbs MOS-674.

### JOIN-MOS-673-03 — мобильное закрытие и footer документации

**Expected современного owner:** `S:38–41,91–99` требует закрывать мобильный sidebar после выбора и задаёт меню документации. MOS-673 самостоятельно не перечисляет эти детали.

**Observed:**

- `application-navigation.tsx:52,67` вызывает `setOpenMobile(false)` для пунктов и документации.
- `app/widgets/navigation/ui/application-navigation/documentation-menu.tsx:35–52` создаёт первые шесть статей, `/docs?article=<id>` и «Все разделы» `/docs`, передаёт `onNavigate`.
- `application-navigation.test.tsx:56–101` содержит keyboard/focus assertions, basename `/tsam-panel`, семь menuitems и закрытие меню.
- `application-navigation.test.tsx:103–148` моделирует ширину 390 и проверяет закрытие drawer после статьи, «Команды» и «Состояние системы».

**Unknown:** физическая геометрия узкого экрана, исполнение в браузере, полный путь root → меню → содержимое статьи. Тест количества/порядка статей использует текущий каталог, а не исторический attachment.

**Вывод:** keep существующего owner MOS-904/shell. Не создавать дополнительную задачу MOS-673 на уже описанное поведение.

## 4. Минимальная диспозиция для parent

| Категория | Решение |
|---|---|
| **keep** | Сохранить существующий shell/navigation owner. Нынешние code/assertions дают содержательное статическое сопоставление member; подтверждённой новой ошибки не установлено. |
| **update** | После независимого review допустимо добавить ссылку на этот отчёт к MOS-673 в аналитическом покрытии. Кандидат U→P означает только частичный member join, не historical parity, feature acceptance или изменение Jira CLOSED. Старые строки/решения не переписывать. |
| **new** | Новый продуктовый change не обоснован. Нельзя дублировать MOS-904/905 или добавлять новые auth/API требования. |
| **question** | Только если потребуется принять именно историческое совпадение: получить разрешённую сохранённую копию вложений `817141/817140` и уточнить авторитетную версию сравнения; `826497` — отдельный исторический result artifact. Это collection/parity gate, не новая политика навигации. |

**Для очереди parent:** продуктовых публикационных кандидатов нет; имеется только кандидат аналитического обновления покрытия. Ничего не опубликовано и не записано в очередь этим worker.

## 5. SHA256 входов

Хеши вычислены локально по полным байтам файлов; hash не означает полного семантического чтения файла. Для `decisions.md` использованы D-008–D-010 и контекст текущей волны; для `S` — строки 28–119.

| Вход | SHA256 |
|---|---|
| `A/work-items/WAVE-D093-LOCAL-EIGHT.md` | `bfed26db7f9865a85e19e0cdfbeb0b92fc7b2b16999be3dac4d1cb92bd5eaf4e` |
| `J` | `30caeb33afa1ae7f9be6c55b9157687174e3bd786dd73a54693e78979b4deef4` |
| `A/sources/jira-shell-details/r1/metadata.json` | `ae842c6c481369e871263f49ad0c58fc9b078ea760c9bb37c20aa400a8854dcb` |
| `A/decisions.md` | `6cce36bc512cc01cd7ef1552fa29676fd385243a37e14720352a0de27564632f` |
| `A/reports/G2-JIRA-MEMBER-JOINS.md` | `dc9b199c2a9500b2ff1857de1feaec9282e8130fa1b78720f551913907618b44` |
| `A/reports/REQ-MOS-904.md` | `5da4177a07799183e526e0c865f09477ea5adad1a467ed486451b7d296b9157b` |
| `A/reports/REQ-MOS-905.md` | `9ed8abd75e53e4667d8123e63721470238d0adb9eb6655f7101105ed2b2127d6` |
| `A/reports/IMPL-MOS-904.md` | `9258bdc25e35134edcfa0d7e484c242be694d9df0c8e1f4988be20f5ab10ee1c` |
| `A/reports/IMPL-MOS-905.md` | `392d18a12350147f7023bf87eeca8d3c244bb29e3592e7d744061a196ba5fdef` |
| `A/reviews/RECON-MOS-904.md` | `014ec43b6596b768840528a93bd89c6d39b5fde422255f3450368db267e403b1` |
| `A/reviews/RECON-MOS-905.md` | `a11af36d27809059d318d2611e92678ad56e132fbe877c6a89c92e88f29d9458` |
| `A/reviews/R-IMPL-MOS-904.md` | `a00671361147dd7ce992d2d32343c26b78743a39f7036d424f5a785b554b8c17` |
| `A/reviews/R-IMPL-MOS-905.md` | `c6702fe75bf0802cc7b181093c7664bb6b00f6878d7ffcc267fae32d082d312e` |
| `S` | `4274bde7ecdf7e18bdcf73cb1755886f3e61bc2cbea3728da0a382006dd0276f` |
| `app/shared/config/constants/application-routes.constants.ts` | `bf50517737722446a5999e1c09ba3b2c603cc837cee23a8ab871e6418c29a21d` |
| `app/shared/config/application-routes.ts` | `db72f56b37d20a92a51e7135167f9944642f7bd2f91965302ac10e1807b42595` |
| `app/shared/config/application-routes.test.ts` | `6201e05d2d1c5fc9606896bcf8dd2782389796dc5a129bb62bbb24cb4fd29213` |
| `app/widgets/navigation/ui/application-navigation.tsx` | `f54dfd66ffe977ce60910a51166fde47363f10d91d81b4da07b9da7473003ff8` |
| `app/widgets/navigation/ui/application-navigation.test.tsx` | `c0b4e5e78802df7c61015822330d4b7f9f510ee254a5efd9686177607dfc2463` |
| `app/widgets/navigation/ui/application-navigation/navigation-entry.tsx` | `6cbf06d9b2dd09b31266b64ce56f24423aea41f4da749a989cfcc1900564ad84` |
| `app/widgets/navigation/ui/application-navigation/documentation-menu.tsx` | `97c173850323d8a5af2e8f005e13d40f71a338375a0b7322012317c3f90ee65e` |
| `app/widgets/navigation/model/get-navigation-item-state.ts` | `83dae90c12d4aafdd86062fbd2086d7bbb32030a99a5d9a1f75aa48f9245998f` |
| `app/application/ui/application-layout.tsx` | `5d4ec467833bece6f0a5f3c96fe61b0355ace670bc8525f726c6b5e6fc021b30` |
| `app/application/constants/application-routes.constants.ts` | `53bc9d61287ea25e292f5410f1905d1718adbefe3f44d6422a6447a183b3230c` |
| `app/routes.ts` | `3b7d7a026d0f73baa121d33407f155cadf9a18ffe5f0a618ad74bc02481594c4` |

## 6. Проверки и остаточные ограничения

Выполнены только локальное чтение, поиск, SHA256/byte-count и проверка сохранённой JSON-структуры. Tests/build/typecheck/lint, network/browser/E2E, бизнес-API и git-команды не запускались. Код, specs, contracts, ledgers и output-файл инструментами не изменялись.

Assertions прочитаны, **не выполнены**. Auth implementation не пересматривалась; новых permission/session решений нет. Шапка MOS-672, breadcrumbs MOS-674, optional internals и бизнес-страницы остаются вне ownership этой lane.

Нет свежести Jira после указанного cutoff, attachment parity, проверки deployed SPA fallback, реальной сессии, backend authorization или deployment текущих байтов. Git index не инспектировался; утверждения `noStagedFiles` нет.