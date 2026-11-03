# IMPL-MOS-961 — точное сопоставление chat/trace/history

## Итог и границы

**В текущем `/sandbox` чат, трассировка и история проверок не реализованы: маршрут непосредственно возвращает общую заглушку.** Существующие компоненты переписки и маршрута принадлежат карточке обычного диалога; их код и тесты не подтверждают выполнение MOS-961.

Проверен только implementation/test boundary MOS-961. MOS-960 (контекст), MOS-962 (синхронизация/токены), права и транспортная политика не переопределялись. Новый аудит требований всего модуля не проводился.

`A` ниже — `openspec/changes/reconcile-control-center-backlog/audit`. Основание: `A/work-items/WAVE-D093-LOCAL-EIGHT.md`, строка IMPL-MOS-961. Предыдущие материалы использованы как карта: `A/reports/SCENARIO-MOS-961.md`, `A/reviews/R-SCENARIO-MOS-961.md`; принятое решение — `A/decisions.md:599–611`, D-012. Исходный отчёт принимается только вместе с поправками review, а не как самостоятельное подтверждение реализации.

## Первичный источник

`A/sources/jira-sandbox-details/r1/content.json#/items/1`:

- `/key`: MOS-961;
- `/description`: ввод и примеры запросов, состояния отправки/ответа; группа/интент, домен, навык, confidence, этика и время этапов; история с временем, автором, результатом и версией;
- там же: transport и формат событий требуется согласовать; HTTP/WebSocket/SSE заранее не выбирать; локальный выбор ответов из трёх строк запрещён;
- `/status`: Backlog;
- `/updated`: `2026-10-15T14:47:13.597+0800`;
- `/retrievedAt`: `2026-10-16T13:18:06.118Z`;
- `/parent`: null; `/comments/total`: 0; `/attachments`: [].

Чтение диапазона файла также показало соседние issue; их описания не использовались для выводов этого отчёта. Membership относится к метаданным сохранения, а не доказывается `parent:null`.

## Новое точное implementation/test evidence

| Область | Expected | Observed: точный locator | Unknown / предел |
|---|---|---|---|
| Чат MOS-961 | Ввод, примеры, отправка и получение ответа | `app/routes/sandbox.tsx:1–5` импортирует только `PlaceholderPage` и возвращает её. `app/pages/placeholder/ui/placeholder-page.tsx:1–10` содержит только «ЦАМ» и «Административная консоль», без формы, сообщений, состояния запроса или истории | Реальная серверная реализация не проверялась. Это доказательство отсутствия сценария в данном UI entrypoint, не отсутствия любого backend |
| Переписка похожего назначения | Нельзя зачесть обычную переписку как sandbox sender | `app/pages/dialog-details/ui/dialog-details/dialog-snapshot.tsx:16–62`: сообщения отображаются из `detail.messages`; вкладки используют один `detail`. `app/entities/dialog/api/dialog-detail-client.ts:14–22`: чтение `/dialogs/v1/dialogs/{chatId}` с проверкой совпадения ID | Этот путь не устанавливает sandbox session identity, команду отправки или формат событий |
| Trace: поля и единицы | Группа/интент, домен, навык, confidence, этика, времена этапов | `app/entities/dialog/api/dialog-detail-schema.ts:94–119`: обычный маршрут содержит `available`, `steps` с `component/action/detail/duration_ms/failed`, серверные `traced_sec/untraced_sec`, действия операторов. `app/pages/dialog-details/ui/dialog-details/dialog-route.tsx:10–53` отображает именно эти значения | Нет основания преобразовать `detail` в классификационные поля или считать `traced_sec` временем sandbox-этапов |
| Trace: существенный и граничный тест | Проверка корректных значений и отличия отсутствующих данных от успеха | `app/pages/dialog-details/ui/dialog-details/dialog-route.test.tsx:40–66`: порядок шагов, равные timestamps, 123 и 0 мс, null и безопасный текст. `:83–114`: серверные totals, null против нуля; доступный пустой маршрут отличается от недоступного | Это прочитанные assertions обычного диалога, не результаты запуска и не sandbox acceptance |
| Processing error | Sandbox-ошибка требует согласованной семантики события/этапа | `dialog-route.test.tsx:68–81` проверяет failed-step, компонент, действие, длительность и fallback при null-пояснении | Не проверяет sandbox `stage/code`, terminal/partial events, ошибки отправки или корреляцию ответа |
| История проверок | Время, автор, результат, версия | В `/sandbox` отсутствует UI истории. `dialog-detail-schema.ts:19–48` описывает автора/время **сообщения**, а `:49–119` — snapshot диалога и маршрут, не запись проверки с result/version | Автор сообщения не подтверждён как автор проверки; timestamp не версия; совместимость истории неизвестна |
| Граница тестового владельца | Не присваивать MOS-961 соседнее покрытие | `app/pages/dialog-details/ui/dialog-details-page.test.tsx:90–124` проверяет единый snapshot при смене вкладок и один fetch. `:126–212` проверяет замену переписки/шагов при refetch; все запросы содержат `/dialogs/v1/dialogs/{chat_id}`, отдельного `/route` нет | Refetch карточки не является подпиской на sandbox events; тесты не проверяют отправку сообщения или историю проверок |

Спецификационная граница подтверждена чтением:

- `openspec/specs/dialog-details/spec.md:9–25`: карточка обычного диалога получает один snapshot, вкладки не создают отдельное чтение; сохраняется предметный смысл сообщений.
- `openspec/specs/skill-checks-training/spec.md:63–70`: `status=sandbox` не доказывает результаты проверок, обработанную версию или доступность песочницы.

Это не новая «спецификация отложенного чата»: D-012 прямо требует не изобретать такую отдельную норму.

## Минимальные решения для очереди parent

1. **keep — MOS-961 остаётся незакрытым.** Сохранённый Backlog и необходимость согласования transport/events не опровергнуты. Текущий entrypoint — заглушка.
2. **update — добавить точное implementation evidence в существующую запись MOS-961:**  
   «`app/routes/sandbox.tsx:1–5` → `PlaceholderPage`, без chat/trace/history; обычный dialog snapshot и его route-тесты не являются реализацией песочницы». Это уточнение доказательств, не новая задача и не новое U→P.
3. **keep — не засчитывать соседнее покрытие.** Оставить обычные диалоги владельцем `DialogSnapshot`, `DialogRoute` и рассмотренных тестов; не переносить их результат на MOS-961.
4. **question — сохранить существующий контрактный вопрос:** transport/events, связь ответа с trace и записью проверки, смысл версии. Источник вопроса — `/items/1/description` и принятый SCENARIO/review; самостоятельно ответ не выбран.
5. **new — не требуется.** Дублирующая задача на тот же чат/trace/history доказательствами не оправдана.

Это только кандидаты для включения parent в `pending-publication.md`. Ничего не опубликовано; очередь инструментами не изменялась.

## Хеши входов

SHA-256 вычислены локально для текущих байтов. Хеш Jira content совпадает с сохранённым metadata.

| Файл | SHA-256 |
|---|---|
| `A/work-items/WAVE-D093-LOCAL-EIGHT.md` | `bfed26db7f9865a85e19e0cdfbeb0b92fc7b2b16999be3dac4d1cb92bd5eaf4e` |
| `A/sources/jira-sandbox-details/r1/content.json` | `4f6db63102f34912d4c50dc39d9f936635054dc805ddfbcf086414d5fe268cb8` |
| `A/sources/jira-sandbox-details/r1/metadata.json` | `685bd0e3937a50ba0ace7e9b810f5ac9a12a67e7d67e9b61b47f8e6fbe51daaf` |
| `A/reports/SCENARIO-MOS-961.md` | `4c8fcea381e7e48c93ff1c2b23e53b76c6115b22b18f2132e63c6165ec9d377f` |
| `A/reviews/R-SCENARIO-MOS-961.md` | `63db3056cd4857ca395ad35951546321599a12c6de369e156d57fb9798e3297d` |
| `A/decisions.md` | `6cce36bc512cc01cd7ef1552fa29676fd385243a37e14720352a0de27564632f` |
| `app/routes/sandbox.tsx` | `c756d932bb442ad34cda9636ba6917e12e3fab57d949dd904432debe993332b3` |
| `app/pages/placeholder/ui/placeholder-page.tsx` | `e39b58ae268a8ef3eb906326cba5cb4e7fc21dba97589fec52090b6b745c5e69` |
| `app/entities/dialog/api/dialog-detail-client.ts` | `ae7839591391c3b32b13a2748918dce670844c15416b95ac490a795a6eb17be9` |
| `app/entities/dialog/api/dialog-detail-schema.ts` | `d28fdf40ef941c9de0a81cfff0f800a14d52fbd7d7f53c33fdddbba45d73443f` |
| `app/pages/dialog-details/ui/dialog-details/dialog-snapshot.tsx` | `1b44bf65b08da39d5106da1479b8a5d9212ae82a890bd47373c9fc5676ea629b` |
| `app/pages/dialog-details/ui/dialog-details/dialog-route.tsx` | `29da1efdd38dcd2671b2201a4999244ebf3f2119fcb6acd3e6f9dd8db9e3fefa` |
| `app/pages/dialog-details/ui/dialog-details/dialog-route.test.tsx` | `58b425f9e3c911033d95fe8fe37620a54a3b33c9f356c4cc153d47b516b99ab7` |
| `app/pages/dialog-details/ui/dialog-details-page.test.tsx` | `b4c956a145dbdbf891813feb7825632f4d6a181c52dc752f9f07b0421092c1bf` |
| `openspec/specs/dialog-details/spec.md` | `25fa6ea2bb92bbcd37ac24d6fb668b6756e7be04dd36d3e23b2abb399d666334` |
| `openspec/specs/skill-checks-training/spec.md` | `9ac5fe8a92ecff214ccdd1998b7d69a2d9083d0bd222ff62541945567c1152cc` |

## Ограничения и проверки

- Historical-source cutoff — сохранение Jira 16.10.2026; актуальность live issue не устанавливалась. Custom fields и тела attachments не собраны; нулевые comments не доказывают отсутствие обсуждений вне capture.
- Предыдущие wiki/API выводы использованы только через принятые report/review/D-012, без повторного whole-module аудита.
- Историческое пользовательское подтверждение MPMM от 09.10.2026 сохраняется согласно D-012; оно не переоткрывается и не расширяется на sandbox transport/deployment. Auth/demo реализация здесь не аудировалась.
- Тесты только прочитаны. Tests/build/typecheck/lint/network/browser/business API не запускались.
- Deployment evidence отсутствует; текущие файлы не доказывают состав развёрнутой сборки. HEAD и git index не проверялись; clean-tree/staging утверждений нет.
- Обязательные локальные источники доступны; blocker для данного сопоставления отсутствует. Файлы инструментами не записывались.