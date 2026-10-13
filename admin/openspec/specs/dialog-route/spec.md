# dialog-route Specification

## Purpose

Отображать реальный маршрут обработки обращения и действия операторов, сохраняя порядок источника и достоверность времени покрытия.

## Requirements

### Requirement: Route is a projection of the accepted detail snapshot

После принятия route-контракта вкладка SHALL использовать route из единой карточки MOS-1041 без отдельного endpoint. Steps SHALL отображаться в порядке источника с occurred_at, kind, component, action, detail, duration_ms, failed. UI MUST NOT генерировать события из messages или выдавать локальные ключи за серверные step IDs. Связи с сообщениями MUST NOT предлагаться без соответствующих данных контракта.

#### Scenario: Equal timestamps

- **WHEN** несколько шагов имеют одинаковое occurred_at
- **THEN** все шаги сохраняются в исходном порядке, без удаления как дубликатов или перестановки по названию компонента

### Requirement: Route kinds and failures are readable

Легенда SHALL различать user_request, platform_module, skill, operator, core. Component/action/detail SHALL показываться как безопасные тексты источника. Failed=true SHALL отображать блок «Сбой обработки» с компонентом и доступным пояснением; отличие MUST NOT выражаться только цветом. Время шага SHALL показываться в согласованном часовом поясе, длительность шага — из duration_ms.

#### Scenario: Failed classification step

- **WHEN** failed=true и detail сообщает причину сбоя классификатора
- **THEN** видны компонент, действие, длительность и текст причины, без синтетического действия «успешно обработано»

### Requirement: Coverage uses server totals

Итоги SHALL использовать route.traced_sec, route.untraced_sec и duration_sec. UI MUST NOT суммировать duration_ms для получения покрытого времени или пересчитывать серверные итоги по переписке. При untraced_sec=0 SHALL показываться полное покрытие; null MUST NOT интерпретироваться как ноль.

#### Scenario: Server total differs from sum of steps

- **WHEN** сумма duration_ms не совпадает с traced_sec
- **THEN** показан серверный traced_sec, а не вычисленная сумма

#### Scenario: Trace exceeds dialog duration

- **WHEN** сервер возвращает traced_sec больше duration_sec и untraced_sec=0
- **THEN** UI сохраняет серверные значения и не создаёт отрицательный непокрытый интервал

### Requirement: Unavailable trace is not an empty trace

При route.available=false вкладка SHALL объяснять недоступность данных без нулевого покрытия и без блокирования переписки. При available=true и steps=[] SHALL показываться отсутствие шагов в полученном маршруте. Смена вкладки MUST NOT перезапрашивать карточку; явный повтор чтения SHALL обновлять согласованный snapshot, а не склеивать маршруты.

#### Scenario: Trace unavailable

- **WHEN** available=false, steps=[] и traced_sec/untraced_sec=null
- **THEN** показана недоступность трассировки, а не «0 шагов, полностью покрыт»

### Requirement: Operator actions preserve their own authors

Operator_actions SHALL показывать occurred_at, operator_id/operator_name, action и details каждого события в исходном порядке. Пустой массив SHALL скрывать блок действий. UI MUST NOT подставлять первого оператора карточки как автора всех действий или генерировать аудит из этих записей.

#### Scenario: Two operators performed actions

- **WHEN** действия принадлежат двум разным operator_id
- **THEN** каждая запись показывает собственного автора и пояснения, даже если её время отличается от accepted_at оператора
