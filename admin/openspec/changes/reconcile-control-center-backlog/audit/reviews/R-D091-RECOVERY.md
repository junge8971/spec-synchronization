# R-D091-RECOVERY — независимое восстановительное review

## Решение

**Принять семь сохранённых отчётов как ограниченные аналитические результаты**, с обязательными ограничениями интеграции ниже. Повторный полный анализ не выполнялся. Повреждённых или пустых drafts нет; оснований для escalate не обнаружено.

Это **не** признание успешными шести failed-запусков, не подтверждение исправления задач и не закрытие глобальных gates. В checkpoint MOS-1166, 1053, 1150, 1054, 1322, 1323 имеют immutable failed provenance: `Subagent produced no output…`. MOS-1167 на момент checkpoint был running; последующий runtime-статус настоящим review не устанавливается. Embedded acceptance в drafts не использовался как доказательство.

Обозначение `A`: `openspec/changes/reconcile-control-center-backlog/audit`.

## Независимая проверка

- HEAD через `git rev-parse HEAD`: `bc0d9800f25a90989b9c73c76f91996f8300f1d3`, соответствует контракту.
- Проверены все **110 строк SHA256** семи отчётов: **103 совпадают**, семь расхождений относятся исключительно к одному `A/coverage.json`. Отсутствующих файлов в таблицах нет.
- Исторический SHA coverage в drafts: `e93adb588725fb39b55f278270ad33e4d7e9da8ac73ee4620d4c0293740d791b`.
- Текущий SHA coverage: `9e25e6c7522d866be6b916e4224ea366416f54eb0eb16db6f9f5ce0e09e5a8e2`.
- Это согласуется с разрешённым D090: `acceptedEvidenceThrough=D-090`, восемь overlays первой волны, `complete=false`; запись прямо исключает принятие second-wave analysts. Прочитан `reviews/R-D090-EIGHT.md`. Старый SHA нельзя заменять задним числом или трактовать как повреждение draft.
- Независимо извлечены исходные descriptions `jira-subtasks/r1/content.json#/items/0,1,13,14,15`. Ключи, родители, содержание и attachment IDs соответствуют отчётам.
- Для MOS-1322/1323 проверены `jira-member-index` items 140/142 и `jira-hierarchy` results 22/23. Description отсутствует; metadata явно исключает его сбор. Поиск точных ключей в сохранённых текстовых sources дал только index/hierarchy.
- Прочитаны решающие текущие owner/code/test участки: surface selection и registration, shell fallback, mock pagination, documentation mobile scroll; для optional-модулей проверен контекст frontend-клиента/queries. Хэш-проверка остальных входов подтверждает неизменность, но не объявляется новым полным семантическим аудитом каждого файла.
- Тесты только читались. Браузер, сеть, серверы, business requests, тестовое выполнение, делегирование и Git mutations не использовались.

## Поотчётные решения

| Draft | Вердикт | Основание, безопасное решение и coverage |
|---|---|---|
| **JOIN-MOS-1166** | **accept** | S(13) действительно требует обрезания длинного описания на «Сценариях». `skill-selection-item.tsx:14–34` выводит `purpose` без локального truncate/clamp; доступное описание сохранено через `aria-describedby`. Main `surface-skill-selection` описывает каталог/выбор, но не это визуальное ограничение. **Допустим U→P** для предметного статического join, не реализации. Разрешено узкое corrective planning визуального ограничения текущего описательного текста; нельзя утверждать воспроизведённый горизонтальный скролл. |
| **JOIN-MOS-1167** | **accept** | S(14) требует появления строки адресов после валидного ввода доменов. `surface-details-step.tsx:58–73` содержит textarea и две статические подсказки, но не зависимый вывод адресов. Это установленный структурный UI-gap; main registration отдельного требования не содержит. **Допустим U→P**. Планировать минимальное отражение введённых доменов; сохранить нормализацию и серверное назначение channel_id. |
| **JOIN-MOS-1053** | **accept** | S(0) задаёт точный document URL `/tsam-panel/skills`, а не все разделы. Main shell содержит соответствующую гарантию; Express и Nginx имеют fallback. В `serve-spa.test.mjs` положительные HTML URL — `/tsam-panel/` и `/tsam-panel/skills/123`; точный URL проверяется только отрицательно с JSON Accept. **Допустим U→P**. Keep реализации/spec; точный положительный regression — необязательное усиление evidence. Deployment остаётся question, нового feature-change не требуется. |
| **JOIN-MOS-1150** | **accept** | S(1) требует шесть элементов при `limit=20&offset=0`, `total_items=6`. `mocks/list.mjs` берёт slice и totals из одного массива; существующий тест действительно использует три элемента. Main owner явно относится к mock. **Допустим U→P только для requirement/API/mock-boundary join**; production/backend execution неизвестен. Не переводить в доказанное backend-покрытие или completion. Keep; необязательный шестимодульный mock regression; question о сохранённом реальном ответе. |
| **JOIN-MOS-1054** | **accept** | S(15) требует мобильного автоскролла после выбора статьи. Main `documentation-search` содержит Manual mobile selection; effect вызывает focus и `scrollIntoView({behavior:'smooth',block:'start'})`; component assertion проверяет именно вызов и фокус. **Допустим U→P** для точного статического join. Keep, новый corrective owner не нужен. Реальная геометрия/устройства/deployment неизвестны. |
| **JOIN-MOS-1322** | **accept** | I(140) содержит только inventory, не body. Наличие KB API/client и принятых capability-отчётов не устанавливает требования этого member. **Сохранить U**, не B/P. Question: получить сохранённый exact issue с provenance; до этого spec/code no-op. Export-limit delta не присваивать MOS-1322. |
| **JOIN-MOS-1323** | **accept** | I(142) аналогично не содержит body. A/B queries подтверждают frontend-интеграцию, но не неизвестный backend scope. **Сохранить U**, не B/P. Question о полном exact issue; никаких требований CRUD/статистики/трафика из заголовка. Сохранить configuration ≠ execution; sample-size delta не присваивать member. |

**P здесь означает bounded substantive partial analysis, а не passed tests, delivery или полное покрытие.** Пять переходов — рекомендация parent для отдельной additive-интеграции; этим review ledger не изменён. Две записи U остаются source gaps. Boundary-оговорки MOS-1150 и optional-модулей нельзя заменять переносом модульного покрытия.

## Минимальные обязательные поправки при интеграции

Переписывать drafts для принятия не требуется. Необходима следующая **additive** фиксация:

1. **Provenance:** связать принятие сохранённых артефактов с настоящим независимым review; сохранить шесть failed runtime-состояний и временную границу checkpoint MOS-1167.
2. **Coverage freshness:** формулировки drafts «coverage сохраняет D-089» считать наблюдением на момент анализа. Текущая база — D-090 с приведённым новым SHA; исторические хэши не исправлять.
3. **MOS-1166:** новый план не должен объявлять `purpose === detail.description`, вводить maxLength=200, detail-fetch, конкретное число строк или tooltip как Jira-требование. Сохранить полный текст и accessibility. Геометрия остаётся непроверенной.
4. **MOS-1167:** preview — только отражение ввода, не подтверждённые серверные адреса/занятость/канал. Не фиксировать URL-схему, кликабельность, точный дизайн или onChange/onBlur как извлечённые acceptance.
5. **MOS-1053 / 1150:** предлагаемые дополнительные тесты — evidence strengthening, не обязательное исправление обнаруженного текущего дефекта. Express-тест не удостоверяет Nginx; mock-тест не удостоверяет backend.
6. **MOS-1054:** не расширять исходное требование до обязательного повторного scroll при выборе той же статьи. Текущий main явно ограничивает сценарий выбором другой статьи.
7. **MOS-1322 / 1323:** не создавать corrective scope и не повышать coverage до получения body. Отсутствие тела в пакете не означает пустое тело в Jira или отсутствие реализации.

Если surface-кандидаты объединяются, сохранить раздельные capability-владельцы `surface-skill-selection` и `surface-registration`; не переносить на них unresolved geometry/target требования MOS-1110/1164/1165 из D090.

## Source gaps и остаточные риски

- Для пяти subtask bodies доступны требования, но отсутствуют attachment bodies, comments и custom acceptance fields. Это не отсутствие самих требований.
- MOS-1150: отсутствует именно JSON ответа 831194, а не только screenshot; идентичности шести модулей не проверены.
- MOS-1166: неизвестны исходный текст/геометрия и точное соответствие старого «описания» текущему полю.
- MOS-1167: отсутствуют изображения 832324/832323; точное визуальное представление неизвестно.
- MOS-1054: видео недоступны; DOM assertion не измеряет действительную прокрутку.
- MOS-1322/1323: отсутствуют сами exact-member bodies; это блокирует substantive requirement-to-implementation join.
- Ни один результат не подтверждает live backend, deployment или успешность тестов. Глобальное завершение reconciliation не следует.

## Отпечатки принятых drafts

Пути относительно `A/reports/`; SHA256 полных байтов:

| Файл | SHA256 |
|---|---|
| JOIN-MOS-1166.md | `189133673f38f2a34c5f4e2b5b6c75993775e592ca59ec90dd52fc6866a92bb5` |
| JOIN-MOS-1167.md | `aff85d24d35b98621db8a2fbabcc74fc16dfa3ca1aa2c04a73a09594cc6eb980` |
| JOIN-MOS-1053.md | `6c7d0a233e6efd50c49721a6417a74fc2c0193b13fee224152dd1c88762eb0d3` |
| JOIN-MOS-1150.md | `6903c1260de201e203d5a012edde1e4ff65d526f7eca264cd45349de8c763f5d` |
| JOIN-MOS-1054.md | `68bdd4e219405f4afc04f832834422b5069f5b87951a36abb53b1a3b6141657d` |
| JOIN-MOS-1322.md | `7a4d665bb17b268b3228a4dbc6d725f8235d7375ab957211a9e8c03b687a87c0` |
| JOIN-MOS-1323.md | `86a89f81d8b8baa87b6566f85abe71e68b0eebb22d1916229db7339de4ef653b` |